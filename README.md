# bluetooth_scan

ラズパイで Bluetooth をスキャンし、Webアプリに送信する。

## インストール

```sell
git clone https://github.com/Tonoyama/bluetooth_scan.git
cd bluetooth_scan
sudo pip3 install -r requirements.txt
```

## cron の設定

```shell
sudo /etc/init.d/cron start
sudo /etc/init.d/cron status
```

```shell
crontab -e
```

1分毎に実行。念の為、事前にスクリプトを実行できるかを確認しておくこと。

```
*/1 * * * * sudo /usr/bin/python3 /home/pi/bluetooth_scan/scan.py
```

書き込まれているかを確認。

```
cronta -l
```

```shell
sudo nano /etc/rsyslog.conf
```

下記のコメントを削除。

```
cron.*                          /var/log/cron.log
```

```shell
sudo /etc/init.d/rsyslog restart
sudo nano /etc/default/cron
```

コメントを削除し、下記のように編集。

```
EXTRA_OPTS='-L 15'
```

```shell
sudo /etc/init.d/cron restart
```

実行されているかを確認。

```
tail -f /var/log/cron.log
```