# Microsoft Rewards 积分快照

这是 [TheNetsky/Microsoft-Rewards-Script](https://github.com/TheNetsky/Microsoft-Rewards-Script) 的独立只读诊断工具：读取上游已有的桌面登录态，记录积分余额、可领取数、可见活动与完成进度。中文和英文仪表盘标签均可识别；`Bing 1/1` 等计数从可访问性进度条读取，避免把旁边的奖励徽章误拼成 `1/11`。

## 用法

先按上游项目说明安装并登录一次。需要 Node.js 22+、上游构建产物、`patchright` 和 `sessions/sessions.db`；本仓库不复制上游或会话数据。

```bash
export REWARDS_ROOT=/path/to/Microsoft-Rewards-Script
export ACCOUNT_1_EMAIL=your_account@example.com
export REWARDS_EVIDENCE_DIR=/private/path/rewards-evidence
node snapshot.cjs
```

可选 `REWARDS_PROXY=http://host:port`；不设置则用默认网络。输出目录包含页面 HTML、截图和账户活动，必须保持私有，不要上传至 Git。`SNAPSHOT_NAME` 可改变 JSON 文件名。

这只是一张状态快照，不执行搜索、答题或领取；退出码 `0` 仅表示读取成功，不表示当日积分已达上限。实际积分应通过上游任务执行前后的余额和活动计数核对。代码遵循上游 GPL-3.0 许可证。

The snapshot also reads fresh authenticated Bing flyout counters into `desktopSearch`, `exploreOnBing`, and `promotionMeta`. These fields contain progress and offer metadata only. An unavailable flyout is recorded as `counterReadError`; old execution logs do not substitute for a current counter read. This remains a read-only adapter.
