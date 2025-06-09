# Button Driver for STM32 HAL (Debounce + Event Handling)

This project implements a modular and reusable **button handling library** in C using **STM32 HAL**. It handles mechanical button debouncing and differentiates between **short press**, **long press (timeout)**, **pressing**, and **release** events through customizable callbacks.

---

## 📁 Files Included

- `Button.c` – Implementation of debouncing logic and event handling.
- `Button.h` – Header defining the `Button_Typdef` structure and function prototypes.

---

## ⚙️ Features

- Debounce handling using a 15ms delay.
- Event callbacks:
  - `btn_pressing_callback()` – Triggered on button press.
  - `btn_press_short_callback()` – Triggered if released within 1000ms.
  - `btn_release_callback()` – Triggered on release.
  - `btn_press_timeout_callback()` – Triggered if pressed for ≥3000ms.
- All callbacks marked with `__weak` so they can be overridden by user-defined functions.

---

## 🧠 How It Works

1. Call `button_init()` to assign GPIO port and pin.
2. Call `button_handle()` in a periodic task (e.g., in a timer interrupt or main loop).
3. Override the `__weak` callbacks in your application code to implement custom behaviour.

---

## ▶️ Example Usage

```c
// Define your own callback
void btn_press_short_callback(Button_Typdef *btn) {
    // Handle short press
}
```

```c
Button_Typdef myButton;
button_init(&myButton, GPIOA, GPIO_PIN_0);

// In main loop or timer
button_handle(&myButton);
```

---

## ⏱ Timing Summary

| Event Type         | Condition                                     |
|--------------------|-----------------------------------------------|
| Debounce           | 15 ms stable input required                   |
| Short Press        | Released within 1000 ms                       |
| Long Press Timeout | Held for 3000 ms                              |

---

## 📌 Notes

- Requires STM32 HAL libraries (for `HAL_GPIO_ReadPin()` and `HAL_GetTick()`).
- Designed to run in any STM32-based embedded system project.

---

## 📤 Author

Developed for STM32 projects that need reliable button input handling and customizable press event detection.
