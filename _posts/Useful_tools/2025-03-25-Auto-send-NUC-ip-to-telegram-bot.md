---
layout:     post
title:      "通过 telegram bot 获取 NUC ip"
subtitle:   "Auto send NUC ip to telegram bot"
date:       2025-03-25 12:05:00
author:     "Xlqmu"
tags:
    - TOOLS
---

上次更新：@2025/03/25 12:15

# 一、前言

1. 默认已有一个telegram账号；
2. 这只是其中一种方法，笔者认为不便外接显示屏情况下最好实现的一种，如读者有更优雅的方法可以来diss笔者；

# 二、Telegram bot
1. 在Telegram搜索BotFather,然后输入/newbot创建自己的bot；
2. 创建成功后，输入/mybot查看自己的api也就是token copy到自己的代码里即可；
3. 点击自己创建的bot开始对话，并且发送任意信息以获取当前chat的id，如果chat不变或者不删除的话id一般是不会变的。


# 三、python脚本示例
``` python 
import smtplib
import subprocess
import requests
import time
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

# 获取 NUC 的 IP 地址(可选，只输出无线ip)
# def get_ip():
#     result = subprocess.run(['ip', 'a'], stdout=subprocess.PIPE, text=True)
#     output = result.stdout
#     for line in output.splitlines():
#         if 'inet' in line and '192.' in line:  
#             return line.split()[1].split('/')[0]
#     return None
def get_ip():
    output = subprocess.check_output(['ip', 'a'], text=True)
    return output

# 通过 Telegram Bot 发送 IP 地址的函数
def send_telegram(ip):
    bot_token = "7882451310:AAGrVvO5P7WKnAKXh7TXOdYzwVnEX7bD6fo"  # 替换为新的 Bot Token

    # 如何获取id

    # https://api.telegram.org/bot{bot_token}/getUpdates"

    # 然后从移动端发送任意信息即可看到id了

    chat_id = 6789293426  # 替换为实际获得的 chat_id
    message_text = f"Your NUC's current IP address is: {ip}"
    url = f"https://api.telegram.org/bot{bot_token}/sendMessage"

    data = {
        "chat_id": chat_id,
        "text": message_text
    }
    try:
        response = requests.post(url, data=data)
        if response.ok:
            print(f"IP address {ip} sent to Telegram chat {chat_id}")
        else:
            print(f"Error sending Telegram message: {response.text}")
    except Exception as e:
        print(f"Exception occurred: {e}")

# 主函数
def main():
    time.sleep(3)  # 等待网络连接建立
    ip = get_ip()
    if ip:
        send_telegram(ip)   # 调用 Telegram Bot 发送函数
    else:
        print("IP address not found!")

if __name__ == "__main__":
    main()
```

# 四、设置开机自启动


``` bash
cat << 'EOF' > ~/.config/autostart/send_ip.desktop
[Desktop Entry]
Type=Application
Exec=bash -c 'for i in {1..3}; do /bin/python3 /home/dji/send_ip.py; done'
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name=Send IP On Login
Comment=Run send_ip.py three times on user login.
EOF
```
ps:内容仅供参考，由于笔者疏懒成性，遂未附上相应图片，还请多多包涵 >_<