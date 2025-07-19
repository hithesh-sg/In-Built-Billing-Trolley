# In-Built Billing Trolley 🛒💡

This project introduces a smart shopping trolley system equipped with an automated billing feature. It leverages **Arduino Uno**, **USB Host Shield**, **Barcode Scanner**, and **16x2 LCD Display** to reduce waiting times at supermarket checkout counters.

## 📌 Abstract

In modern retail environments, long queues at billing counters frustrate customers. This project aims to solve that by integrating an automated billing mechanism directly into the trolley. The customer scans each item before placing it into the basket, and the system updates the cost and item count in real time.

## 🛠️ Hardware Used

- Arduino Uno
- USB Host Shield
- Barcode Scanner
- 16x2 LCD Display (I2C)
- Basket (physical trolley)
- Power Supply

## 🧠 Features

- Real-time item name and price display
- Total cost and item count updates
- Option to remove wrongly added items
- Alerts for invalid/unregistered barcodes
- Simple and intuitive LCD UI

## 📦 Installation & Setup

1. Connect the barcode scanner to Arduino via the USB Host Shield.
2. Connect the LCD display using I2C.
3. Upload the code from the `source_code/` folder to Arduino Uno.
4. Power the circuit via USB or battery.
5. Scan products and watch the billing on the LCD.

## 🔄 Workflow

1. User scans an item.
2. LCD displays item name and price.
3. System tracks total items and cost.
4. Removing items updates the total accordingly.

## 🔗 References

- IEEE Xplore research articles on smart billing systems
- Arduino official docs
- Adafruit & SparkFun tutorials

## 👨‍💻 Authors

- SG. Hithesh (22H51A04B9)

## 📜 License

This project is licensed under the MIT License.
