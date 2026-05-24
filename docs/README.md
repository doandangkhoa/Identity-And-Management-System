# Tài liệu và sơ đồ

Thư mục `docs` được chia theo loại tài liệu để dễ tìm và dễ render sơ đồ.

## Cấu trúc

```
docs/
├── reports/
│   ├── bao_cao_phan_tich_thiet_ke_he_thong_iam_mfa.md
│   └── SRS.md
├── planning/
│   ├── work_allocation.md
│   └── work_allocation.odt  # chuyển vào đây sau khi file không bị khóa
└── diagrams/
    ├── use-case/
    ├── activity/
    ├── class/
    ├── sequence/
    │   └── legacy/
    ├── communication/
    ├── object/
    └── state/
```

## File hay dùng

- Sơ đồ lớp chi tiết: `diagrams/class/class_diagram.puml`
- Ảnh render sơ đồ lớp: `diagrams/class/IAM_MFA_Class_Diagram.png`
- Sơ đồ lớp domain/service/event: `diagrams/class/class_domain_diagram.puml`
- Sơ đồ lớp DAM/DAO repository: `diagrams/class/class_dam_dao_diagram.puml`
- Báo cáo chính: `reports/bao_cao_phan_tich_thiet_ke_he_thong_iam_mfa.md`
- Phân công nhiệm vụ: `planning/work_allocation.md`

Lưu ý: nếu `work_allocation.odt` đang mở trong LibreOffice/Word, Windows có thể giữ file ở thư mục gốc cho đến khi đóng ứng dụng.

## Render PlantUML

Render một file:

```powershell
java -jar tools\plantuml\plantuml.jar docs\diagrams\class\class_diagram.puml
```

Render toàn bộ sơ đồ:

```powershell
java -jar tools\plantuml\plantuml.jar "docs\diagrams\**\*.puml"
```
