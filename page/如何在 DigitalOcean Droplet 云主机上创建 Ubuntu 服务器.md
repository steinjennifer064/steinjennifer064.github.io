在本文中，你将学习如何通过 DigitalOcean 的管理面板创建一个 Ubuntu 服务器，并将其配置为使用你的 SSH 密钥。设置好服务器后，你可以在其上部署应用程序和网站。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

---

## 本文内容包括：
1. 准备工作
2. 创建 DigitalOcean 帐户
3. 设置 Droplet
4. 选择操作系统镜像
5. 选择计划
6. 添加块存储（可选）
7. 选择数据中心区域
8. 设置 SSH 身份验证
9. 完成并创建 Droplet

---

## 准备工作

在开始本教程之前，请确保满足以下条件：

- **对命令行有一定的了解**：如果需要复习，可以参考 [Linux 命令行入门](https://www.digitalocean.com/community/tutorials/a-linux-command-line-primer)。
- **SSH 密钥**：用于启用与服务器的安全连接。你可以参考 [如何在 Ubuntu 上设置 SSH 密钥](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04)。
- **信用卡或 PayPal 帐户**：用于设置 DigitalOcean Droplet 云主机。

---

## 步骤 1 — 创建 DigitalOcean 帐户

要访问 DigitalOcean 控制面板并创建 Droplet 云主机，你需要一个 DigitalOcean 帐户。请前往 [DigitalOcean 新帐户注册页面](https://bit.ly/bewildcard) 创建新帐户。你可以选择通过电子邮件、Google 或 GitHub 注册。

完成注册后，输入信用卡或 PayPal 信息以验证身份。验证完成后，你将进入“注册完成”页面，点击“让我们做点什么（Let’s make something）”按钮，继续下一步。

---

## 步骤 2 — 设置你的 Droplet

在控制面板中，点击右上角的“创建（Create）”菜单，然后选择“Droplet”以打开 Droplet 创建页面。在这里，你可以选择 Droplet 的配置，包括操作系统、内存、存储等。

---

## 步骤 3 — 选择操作系统镜像

在 Droplet 创建页面中，选择操作系统镜像。由于本教程用于设置 Ubuntu，请选择 **Ubuntu (LTS) x64** 选项。

---

## 步骤 4 — 选择计划

在“选择计划”部分，你可以选择 Droplet 的 RAM、存储空间和 CPU 核心数。如果你是初学者，建议选择每月 5 美元的基础计划。稍后你可以根据需要随时升级。

---

## 步骤 5 — 添加块存储（可选）

如果需要额外的文件存储空间，可以在此步骤中添加块存储。此选项是可选的，具体取决于你的需求。

---

## 步骤 6 — 选择数据中心区域

选择一个距离你和你的用户最近的数据中心，以获得最佳性能和最小延迟。

---

## 步骤 7 — 选择其他选项

在“选择其他选项”部分，你可以启用以下功能：
- **IPv6**：为 Droplet 启用 IPv6 访问。
- **用户数据**：指定任意数据，用于初始化 Droplet。
- **监控**：启用 DigitalOcean 监控功能，收集扩展指标。

这些功能是免费的，可以根据需要启用。

---

## 步骤 8 — 设置 SSH 身份验证

使用 SSH 密钥进行身份验证，这比密码更安全。点击“新建 SSH 密钥”按钮，将你的公共 SSH 密钥粘贴到弹出窗口中，然后点击“添加新 SSH 密钥”。

如果尚未创建 SSH 密钥，可以参考 [如何在 Ubuntu 上设置 SSH 密钥](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04)。

---

## 步骤 9 — 完成并创建 Droplet

在最后一步中，你可以：
- 选择要创建的 Droplet 数量（通常为 1 个）。
- 命名 Droplet。
- 添加标签或分配到项目（可选）。
- 启用备份（每月额外 1 美元）。

完成后，点击“创建 Droplet”。创建完成后，你将获得 Droplet 的 IP 地址。通过以下命令以 `root` 用户身份连接到 Droplet：

bash
ssh root@your_IP_address


---

## 结论

在本教程中，你已成功在 DigitalOcean Droplet 上设置了 Ubuntu 服务器并启用了 SSH 访问。接下来，你可以部署应用程序或网站。如果需要进一步优化服务器设置，可以参考 [初始服务器设置教程](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu)。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)