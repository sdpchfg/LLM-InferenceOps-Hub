# 版本检查与自动更新

## 版本检查流程

### 1. 读取本地版本

首先读取本地版本信息：

```bash
cat version.json
```

本地版本格式：
```json
{
  "local_version": "1.0.0",
  "last_checked": "2026-04-20",
  "cache_validity_hours": 24
}
```

### 2. 检查更新

检查远程版本URL（用户需要替换为自己的GitHub仓库地址）：
```
https://raw.githubusercontent.com/{owner}/{repo}/main/version.json
```

### 3. 版本比较

版本号格式：MAJOR.MINOR.PATCH

- **MAJOR**: 不兼容的API变更
- **MINOR**: 向后兼容的功能新增
- **PATCH**: 向后兼容的问题修复

### 4. 更新执行

当发现新版本时：

1. **提示用户**：告知有新版本可用
2. **显示变更**：列出更新内容
3. **确认更新**：用户确认后执行更新
4. **验证更新**：确认更新成功

## 更新状态管理

| 状态 | 说明 |
|------|------|
| `up_to_date` |已是最新版本 |
| `update_available` | 发现新版本 |
| `update_required` | 必须更新（安全修复） |
| `check_failed` | 版本检查失败 |

## 自动更新优势

1. **用户无感知**：更新在后台完成，用户无需手动操作
2. **版本一致性**：所有用户使用相同版本
3. **热更新**：SKILL内容更新后立即生效
4. **版本回滚**：如有问题可快速回滚

## GitHub集成（推荐）

为实现自动更新，建议将SKILL发布到GitHub：

1. 创建公开仓库
2. 将整个项目目录内容推送到仓库
3. 用户克隆仓库后即可使用
4. 更新时只需推送新版本，用户下次使用时自动检查

## 版本发布流程

```bash
# 1. 更新版本号
# 编辑 version.json

# 2. 更新SKILL.md中的版本信息
# 编辑 SKILL.md 顶部的版本信息

# 3. 提交并推送
git add .
git commit -m "Release v1.0.1: [描述更新内容]"
git push

# 4. 创建GitHub Release（可选）
gh release create v1.0.1 --title "v1.0.1" --notes "[更新内容]"
```

## 版本检查代码示例

```javascript
// version-check.js
const fs = require('fs');
const https = require('https');

const LOCAL_VERSION_PATH = './version.json';
const REMOTE_VERSION_URL = 'https://raw.githubusercontent.com/{owner}/{repo}/main/version.json';

async function checkForUpdates() {
  const localData = JSON.parse(fs.readFileSync(LOCAL_VERSION_PATH, 'utf8'));
  const localVersion = localData.version;

  const remoteData = await fetchRemoteVersion(REMOTE_VERSION_URL);
  const remoteVersion = remoteData.version;

  if (compareVersions(remoteVersion, localVersion) > 0) {
    console.log(`新版本可用: ${remoteVersion} (当前: ${localVersion})`);
    console.log('更新内容:', remoteData.changelog);
    return { updateAvailable: true, remoteVersion, localVersion };
  }

  return { updateAvailable: false };
}

function compareVersions(v1, v2) {
  const parts1 = v1.split('.').map(Number);
  const parts2 = v2.split('.').map(Number);
  for (let i = 0; i < 3; i++) {
    if (parts1[i] > parts2[i]) return 1;
    if (parts1[i] < parts2[i]) return -1;
  }
  return 0;
}
```

## 使用者无需更新的原因

1. **SKILL内容在对话中加载**：SKILL的所有内容都直接存在于SKILL.md中
2. **版本检查机制**：Trae AI会在需要时检查版本
3. **中心化更新**：只需更新源仓库，使用者自动获取最新版本
4. **无需重新安装**：SKILL无需下载/安装/更新，即用即生效
