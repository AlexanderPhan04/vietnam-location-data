# 🇻🇳 Vietnam Location Data

A comprehensive, structured database of Vietnamese administrative divisions including provinces, districts, wards, postal codes, and area codes.

[![GitHub](https://img.shields.io/badge/GitHub-vietnam--location--data-blue?logo=github)](https://github.com/AlexanderPhan04/vietnam-location-data)

## 📖 Overview

This project provides detailed location data for Vietnam's administrative divisions in JSON format. The data includes:

- **63 provinces and centrally-governed cities** (Tỉnh/Thành phố trực thuộc Trung ương)
- Districts, counties, towns (Quận/Huyện/Thị xã/Thành phố)
- Wards, communes, townships (Phường/Xã/Thị trấn)
- Postal codes (Mã bưu chính)
- Area codes (Mã vùng điện thoại)
- Geographic regions and descriptions

## 📂 Project Structure

```
vietnam-location-data/
├── README.md
└── VN/
    ├── HaNoi/
    │   └── HaNoi.json
    ├── HoChiMinh/
    │   └── HoChiMinh.json
    ├── DaNang/
    │   └── DaNang.json
    ├── CaMau/
    │   └── CaMau.json
    └── ... (63 provinces total)
```

Each province has its own folder containing a JSON file with complete administrative data.

## 🗂️ Data Structure

### Province Level

```json
{
  "province": {
    "id": "VN-HN",
    "code": "HN",
    "name": "Hà Nội",
    "type": "Thành phố trực thuộc Trung ương",
    "region": "Miền Bắc",
    "slug": "ha-noi",
    "description": "Optional description",
    "area_code": "024",
    "postal_code": {
      "type": "range",
      "value": ["100000", "150000"],
      "note": "Optional note"
    }
  },
  "units": [
    /* Districts array */
  ]
}
```

### District Level

```json
{
  "id": "HN-BD",
  "code": "BD",
  "name": "Ba Đình",
  "type": "Quận",
  "type_code": "URBAN_DISTRICT",
  "area_code": "024",
  "postal_code": ["111000", "111999"],
  "note": "Optional note",
  "wards": [
    /* Wards array */
  ]
}
```

### Ward Level

```json
{
  "id": "HN-BD-PH",
  "code": "PH",
  "name": "Phúc Xá",
  "type": "Phường",
  "type_code": "WARD",
  "postal_code": "111100",
  "note": "Optional note"
}
```

## 🏷️ Type Codes

### Province Types

- **Thành phố trực thuộc Trung ương**: Centrally-governed cities (Hà Nội, Hồ Chí Minh, Đà Nẵng, Cần Thơ, Hải Phòng)
- **Tỉnh**: Provinces

### District Types

- **URBAN_DISTRICT** (Quận): Urban districts
- **RURAL_DISTRICT** (Huyện): Rural districts
- **MUNICIPAL_CITY** (Thành phố): Municipal cities
- **CITY** (Thành phố): Cities
- **TOWN** (Thị xã): Towns

### Ward Types

- **WARD** (Phường): Wards (urban areas)
- **COMMUNE** (Xã): Communes (rural areas)
- **TOWNSHIP** (Thị trấn): Townships

## 📍 Regions

Vietnam is divided into several main regions:

- **Miền Bắc**: Northern Vietnam
- **Miền Trung**: Central Vietnam
- **Miền Nam**: Southern Vietnam
- **Đồng bằng sông Cửu Long**: Mekong Delta
- **Duyên hải Nam Trung Bộ**: South Central Coast

## 🚀 Usage

### Reading a Province File

```javascript
// Node.js
const fs = require("fs");
const hanoiData = JSON.parse(fs.readFileSync("./VN/HaNoi/HaNoi.json", "utf8"));

console.log(hanoiData.province.name); // "Hà Nội"
console.log(hanoiData.province.area_code); // "024"
console.log(hanoiData.units.length); // Number of districts
```

```python
# Python
import json

with open('./VN/HaNoi/HaNoi.json', 'r', encoding='utf-8') as f:
    hanoi_data = json.load(f)

print(hanoi_data['province']['name'])  # "Hà Nội"
print(hanoi_data['province']['area_code'])  # "024"
print(len(hanoi_data['units']))  # Number of districts
```

### Finding a Specific Ward

```javascript
const data = require("./VN/HoChiMinh/HoChiMinh.json");

// Find district
const district = data.units.find((u) => u.code === "TD");
console.log(district.name); // "Thủ Đức"

// Find ward
const ward = district.wards.find((w) => w.code === "TT");
console.log(ward.name); // "Thủ Thiêm"
console.log(ward.postal_code); // "713100"
```

## 📦 Available Provinces

<details>
<summary>View all 63 provinces (click to expand)</summary>

### Northern Vietnam (Miền Bắc)

- Hà Nội (HN)
- Hải Phòng (HP)
- Hưng Yên (HY)
- Bắc Ninh (BN)
- Thái Nguyên (TN)
- Lạng Sơn (LS)
- Cao Bằng (CB)
- Lào Cai (LC)
- Điện Biên (DB)
- Lai Châu (LC)
- Sơn La (SL)
- Phú Thọ (PT)
- Tuyên Quang (TQ)
- Ninh Bình (NB)
- Thanh Hóa (TH)
- Nghệ An (NA)
- Hà Tĩnh (HT)

### Central Vietnam (Miền Trung)

- Đà Nẵng (DN)
- Huế (HU)
- Quảng Trị (QT)
- Quảng Ngãi (QN)
- Khánh Hòa (KH)
- Lâm Đồng (LD)
- Đắk Lắk (DL)
- Gia Lai (GL)

### Southern Vietnam (Miền Nam)

- Hồ Chí Minh (SG)
- Đồng Nai (DN)
- Bình Dương (BD)
- Tây Ninh (TN)
- Long An (LA)
- Tiền Giang (TG)
- Bến Tre (BT)
- Trà Vinh (TV)
- Vĩnh Long (VL)
- Đồng Tháp (DT)
- An Giang (AG)
- Kiên Giang (KG)
- Cần Thơ (CT)
- Hậu Giang (HG)
- Sóc Trăng (ST)
- Bạc Liêu (BL)
- Cà Mau (CM)

_And more..._

</details>

## 🔍 Features

✅ Complete administrative hierarchy (Province → District → Ward)  
✅ Unique IDs for each administrative unit  
✅ Vietnamese and ASCII slug names  
✅ Postal codes (single values and ranges)  
✅ Area codes for phone numbers  
✅ Type classifications with standardized codes  
✅ Regional groupings  
✅ Optional descriptions and notes  
✅ UTF-8 encoded with proper Vietnamese characters

## 📝 Data Quality

- All data follows a consistent JSON structure
- Each administrative unit has a unique identifier
- Postal codes are verified for major cities
- Area codes are accurate as of 2025
- Data is regularly maintained and updated

## 🤝 Contributing

Contributions are welcome! If you find any errors or want to add missing data:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/update-data`)
3. Make your changes
4. Commit your changes (`git commit -am 'Update [Province] data'`)
5. Push to the branch (`git push origin feature/update-data`)
6. Open a Pull Request

## 📄 License

This project is open source and available for public use. Please credit this repository if you use the data in your projects.

## 🔗 Links

- **Repository**: [https://github.com/AlexanderPhan04/vietnam-location-data](https://github.com/AlexanderPhan04/vietnam-location-data)
- **Issues**: [Report bugs or suggest improvements](https://github.com/AlexanderPhan04/vietnam-location-data/issues)

## 💡 Use Cases

- Address autocomplete systems
- E-commerce shipping forms
- Government applications
- Geographic data analysis
- Location-based services
- Postal code validation
- Phone number validation

## 📊 Statistics

- **63** Provinces/Cities
- **700+** Districts
- **10,000+** Wards/Communes
- Complete postal code coverage
- Full area code mapping

---

**Made with ❤️ for Vietnam** | Last updated: December 2025
