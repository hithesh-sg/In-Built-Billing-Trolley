#include <hidboot.h>
#include <hiduniversal.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

String DataBarcode;
bool x = false;

struct Product {
  String barcode; // Barcode for the product
  String name;    // Name of the product
  float cost;     // Cost of the product
};

Product products[10] = {
  {"5449000234612", "Sprite 1L", 100},
  {"6009510806151", "Lays 105G", 50},
  {"8992760221028", "Oreo 18G", 10},
  {"5449000054227", "Coke 1L", 100},
  {"6001068587209", "Maggie 73G", 14},
  {"4902430510899", "Tide 1Kg", 138},
  {"8901399111013", "Santoor soap", 35},
  {"6001067066613", "Colgate 100G", 69},
  {"8901030406256", "Gemini Tea 500G", 265},
  {"8901725121181", "Atta 5KG", 244},
};

float Titems = 0;
float Tcost = 0;

class KbdRptParser : public KeyboardReportParser {
  void PrintKey(uint8_t mod, uint8_t key);
protected:
  void OnControlKeysChanged(uint8_t before, uint8_t after);
  void OnKeyDown(uint8_t mod, uint8_t key);
  void OnKeyUp(uint8_t mod, uint8_t key);
  void OnKeyPressed(uint8_t key);
};

void KbdRptParser::PrintKey(uint8_t m, uint8_t key) {
  MODIFIERKEYS mod;
  ((uint8_t)&mod) = m;
}

void KbdRptParser::OnKeyDown(uint8_t mod, uint8_t key) {
  PrintKey(mod, key);
  uint8_t c = OemToAscii(mod, key);
  if (c)
    OnKeyPressed(c);
}

void KbdRptParser::OnControlKeysChanged(uint8_t before, uint8_t after) {
  MODIFIERKEYS beforeMod;
  ((uint8_t)&beforeMod) = before;
  MODIFIERKEYS afterMod;
  ((uint8_t)&afterMod) = after;
}

void KbdRptParser::OnKeyUp(uint8_t mod, uint8_t key) {
  // No action on key release
}

void KbdRptParser::OnKeyPressed(uint8_t key) {
  if (key == 0x0D) {
    x = true;
  } else {
    DataBarcode += (char)key;
  }
}

USB Usb;
HIDUniversal Hid(&Usb);
KbdRptParser Prs;

void setup() {
  Serial.begin(115200);
  Serial.println("Start");
  if (Usb.Init() == -1)
    Serial.println("OSC did not start.");

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("WELCOME");
  lcd.setCursor(0, 1);
  lcd.print("START SCANNING");
  delay(400);
  lcd.clear();

  Hid.SetReportParser(0, &Prs);
}

void loop() {
  Usb.Task();

  if (x) {
    Serial.println(DataBarcode);
    LCDProductDetails(DataBarcode);
    delay(400);
    lcd.clear();
    x = false;
    DataBarcode = "";
  }

  lcd.setCursor(0, 0);
  lcd.print("Items: " + String(Titems));
  lcd.setCursor(0, 1);
  lcd.print("Amount: " + String(Tcost));
  delay(200);
  lcd.clear();
}

void LCDProductDetails(String barcode) {
  for (int i = 0; i < 10; i++) {
    if (products[i].barcode == barcode) {
      lcd.setCursor(0, 0);
      lcd.print(products[i].name);
      Titems++;
      lcd.setCursor(0, 1);
      lcd.print(products[i].cost);
      Tcost = Tcost + products[i].cost;
      return;
    }
  }
  Serial.print("Invalid Barcode");
  // Optionally display on LCD:
  // lcd.setCursor(0, 0);
  // lcd.print("Invalid");
  // delay(500);
  // lcd.clear();
}
