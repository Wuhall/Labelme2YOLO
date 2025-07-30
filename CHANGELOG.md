# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Fixed
- **增强图像处理健壮性**: 修复了当 Labelme JSON 文件中缺少 `imageData` 字段或该字段为空时程序崩溃的问题
  - 新增备用方案：当 `imageData` 不可用时，自动从本地目录查找同名图片文件并复制，*这里的前提是label与image在同级目录*
  - 支持多种常见图片格式：`.png`, `.jpg`, `.jpeg`, `.bmp`, `.tiff`
  - 保持向后兼容性：优先使用原有的 base64 解码逻辑
  - 改进错误处理：提供更清晰的中文错误信息

### Technical Details
- 修改了 `_save_yolo_image()` 方法中的图像处理逻辑
- 添加了条件检查来验证 `imageData` 字段的存在性和有效性
- 实现了基于文件系统的图像复制备用机制
- 增强了异常处理，提供更友好的错误提示

### Impact
- 提高了工具对不同类型 Labelme 标注文件的兼容性
- 减少了因缺少 `imageData` 导致的转换失败情况
- 改善了用户体验，特别是处理外部图片文件时的稳定性 