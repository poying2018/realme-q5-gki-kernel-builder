# Realme Q5 GKI内核编译 - 完整计划

## 已完成的工作

我已经创建了完整的GitHub Action工作流，用于编译真我Q5的GKI内核并集成KernelSU root功能。

### 文件结构
```
realme-q5-gki-kernel-builder/
├── .github/
│   └── workflows/
│       └── build-gki-kernel.yml    # GitHub Action工作流
└── README.md                       # 项目说明文档
```

## GitHub Action功能

### 1. 编译配置选项
- **内核分支**: 支持选择不同的内核源码分支
- **KernelSU**: 可选是否集成KernelSU root功能
- **SUSFS**: 可选是否集成SUSFS系统修改功能
- **LTO模式**: 支持thin/full/none三种优化模式

### 2. 编译流程
1. **环境准备**: 安装编译依赖，配置AOSP Clang工具链
2. **源码同步**: 从Realme官方仓库同步内核源码
3. **内核补丁**: 应用Realme Q5设备特定的补丁
4. **KernelSU集成**: 自动安装KernelSU root解决方案
5. **内核配置**: 使用gki_defconfig配置内核
6. **编译内核**: 使用Clang编译GKI内核
7. **打包发布**: 使用AnyKernel3打包，自动创建Release

### 3. 编译产物
- **AnyKernel3刷入包**: 包含内核Image和dtbo.img
- **自动Release**: 编译成功后自动创建GitHub Release
- **Artifacts**: 保存编译产物30天

## 下一步操作

### 步骤1: 创建GitHub仓库
1. 登录GitHub账号
2. 点击右上角"+" → "New repository"
3. 仓库名称: `realme-q5-gki-kernel-builder`
4. 描述: `GitHub Action for building GKI kernel for Realme Q5 (oscar)`
5. 选择**Public**（推荐）或Private
6. 点击"Create repository"

### 步骤2: 上传文件到仓库
在GitHub仓库页面:
1. 点击"uploading an existing file"
2. 拖拽或选择以下文件:
   - `README.md`
   - `.github/workflows/build-gki-kernel.yml`
3. 点击"Commit changes"

### 步骤3: 启用GitHub Actions
1. 进入仓库的"Actions"标签页
2. 点击"I understand my workflows, go ahead and enable them"
3. 工作流会自动启用

### 步骤4: 运行编译
1. 在"Actions"标签页选择"Build Realme Q5 GKI Kernel"
2. 点击"Run workflow"
3. 配置选项:
   - **kernel_branch**: `master`（默认）
   - **enable_kernelsu**: `true`（启用root）
   - **enable_susfs**: `false`（可选）
   - **lto_mode**: `thin`（推荐）
4. 点击"Run workflow"

### 步骤5: 等待编译完成
- 编译时间: 约30-60分钟
- 可以点击工作流查看实时日志
- 编译成功后会自动创建Release

### 步骤6: 下载和刷入内核
1. 进入"Releases"标签页
2. 下载最新的AnyKernel3 zip文件
3. 刷入方法:
   - **方法1 (推荐)**: Recovery模式下adb sideload
   - **方法2**: Fastboot模式直接刷入

## 技术细节

### 内核源码
- **官方源码**: https://github.com/realme-kernel-opensource/realme_9pro-5G_9-5G_V25_Q5-AndroidS-kernel-source
- **GKI版本**: android12-5.10
- **Defconfig**: gki_defconfig

### KernelSU集成
- **安装命令**: `curl -LSs https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh | bash -`
- **管理器下载**: https://github.com/tiann/KernelSU/releases

### 设备信息
- **代号**: oscar
- **SoC**: 高通骁龙695 (SM6375)
- **架构**: arm64
- **内核版本**: 5.10 (Android 12)

## 注意事项

### 首次编译
- 首次编译可能需要较长时间（约1小时）
- 建议先测试编译是否成功
- 可以先禁用KernelSU进行测试

### 常见问题
1. **编译失败**: 检查日志，可能是源码兼容性问题
2. **刷入后无法开机**: 尝试不同的LTO模式或恢复原厂内核
3. **KernelSU不工作**: 确保安装了KernelSU管理器APK

### 优化建议
- 使用`thin` LTO模式可以加快编译速度
- 启用ccache可以加速后续编译
- 可以根据需要调整defconfig选项

## 相关资源

- [Realme官方内核源码](https://github.com/realme-kernel-opensource)
- [KernelSU官方文档](https://kernelsu.org/guide/installation.html)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP GKI文档](https://source.android.com/docs/core/architecture/kernel/generic-kernel-image)
