# Remote Stack Safety Monitor
基于 SSH 远程监控 Linux 进程栈内存使用状态。采用 SSH 远程采集 + 本地分析 的解耦架构，确保对生产环境零侵入。通过本地电脑远程登录目标服务器，采集指定进程的栈内存限制与实际使用量，计算使用率并与预设阈值对比，精准判断运行过程中是否出现过因循环嵌套过深等原因导致的栈内存占用过大、栈溢出风险，生成结构化 JSON 报告检测结果保存在本地。


## 项目目录结构

remote-stack-monitor/
1. .gitignore            # Git忽略文件
2. README.md             # 项目说明文档
3. requirements.txt      # 依赖库清单
4. config.py             # 配置管理
5. ssh_client.py         # SSH客户端封装
6. analyzer.py           # 栈分析器
7. reporter.py           # 报告生成器
8. main.py               # 主程序
9.  report.json           # 示例报告（最终检测报告）                         

## 功能特性
- 远程获取进程栈内存数据；
- 解析smaps文件提取栈段最大占用量（包括:Size,  RSS, Swap）；
- 计算使用率并与阈值对比，判定风险等级；
- 生成JSON格式报告；
- 支持环境变量/命令行参数灵活配置；
- 完善的异常处理与日志记录。

## 快速开始
### 1. 环境准备
```bash
# 克隆仓库
git clone https://github.com/yanshizhao/StackSentinel.git
cd StackSentinel

# 安装依赖
pip install -r requirements.txt

# 执行程序
python main.py --host <目标服务器ip> --port <端口号> --user <目标服务器用户名> --password <目标服务器登录密码> --pid <目标进程>