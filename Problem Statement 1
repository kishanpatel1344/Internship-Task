Global Variables

#include "stm32f1xx_hal.h"

// Global variables

volatile uint8_t g_ReadDIpinSts = 0x00;

volatile uint8_t g_AppDIpinSts = 0x00;

static uint8_t consistency_counter[8] = {0};

// Function prototypes

void CAN_Config(void);

void GPIO_Config(void);

void Error_Handler(void);

ISR Code

void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin) {

 static uint32_t lastISRTime = 0;

 // Read digital input status

 g_ReadDIpinSts = 0x00; // Clear the status register

 for (int i = 0; i < 8; i++) {

 if (HAL_GPIO_ReadPin(GPIOB, (GPIO_Pin_0 << i)) == GPIO_PIN_SET) {

 g_ReadDIpinSts |= (1 << i); // Set the corresponding bit

 }

 }

 // Update digital input status based on consistency

 for (int i = 0; i < 8; i++) {

 if ((g_ReadDIpinSts & (1 << i)) == (g_AppDIpinSts & (1 << i))) {

 if (consistency_counter[i] < 10) {

 consistency_counter[i]++;

 }

 } else {

 consistency_counter[i] = 0;

 }

 if (consistency_counter[i] >= 10) {

 g_AppDIpinSts |= (1 << i); // Update the status

 } else {

 g_AppDIpinSts &= ~(1 << i); // Clear the status

 }

 }

 // Update CAN message here

 CAN_UpdateMessage(g_AppDIpinSts);

}

void CAN_UpdateMessage(uint8_t status) {

 // Implement CAN communication code here

 // Example: Transmit `status` over CAN

}

CAN Configuration

void CAN_Config(void) {

 CAN_HandleTypeDef hcan;

 hcan.Instance = CAN1;

 hcan.Init.Prescaler = 16;

 hcan.Init.Mode = CAN_MODE_NORMAL;

 hcan.Init.SJW = CAN_SJW_1TQ;

 hcan.Init.BS1 = CAN_BS1_6TQ;

 hcan.Init.BS2 = CAN_BS2_8TQ;

 hcan.Init.TTCM = DISABLE;

 hcan.Init.ABOM = DISABLE;

 hcan.Init.ABS = DISABLE;

 hcan.Init.OME = DISABLE;

 hcan.Init.TS = DISABLE;

 HAL_CAN_Init(&hcan);

 // Configure CAN filters here

}
