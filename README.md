import subprocess
import hashlib
import time
def run(cmd):
    try:
        out = subprocess.check_output(cmd, shell=True, stderr=subprocess.DEVNULL)
        return out.decode().strip()
    except Exception:
        return ""

android_id = run("settings get secure android_id")
serial = run("getprop ro.serialno") or run("getprop ro.boot.serialno") or run("getprop ro.hardware")
brand = run("getprop ro.product.brand")
model = run("getprop ro.product.model")
mac = run("cat /sys/class/net/wlan0/address 2>/dev/null")
values = [v for v in [android_id, serial, brand, model, mac] if v]
concat = "|".join(values)

SALT = "سِرّ_خاص_قوي_غير_مُشارَك"

full = SALT + "|" + concat
h = hashlib.sha256(full.encode()).hexdigest()
hash=['641427704b311baafb1888f5f9f5c649359e18917c57e3b860e55213a93348e4','294b6221ca2add3f64f9d583b20bce571fc61daf1acb85687b4d73342d1b6c53','5492156e8956344a4cfd3ec430368d2d85a4c8fca36ce8a4ca7e2f30f6eb25b0','47cd5862c047b309cc5b57bff52c978b4a30b7025f249365cd2742b5091d2a5c','5492156e8956344a4cfd3ec430368d2d85a4c8fca36ce8a4ca7e2f30f6eb25b0','2239da2340b1b0943232f0b0cc1a536a2bb2876329e50fb51c283db705cea175','1eb2a4e0a5e85df1df8e8702753935d9ce379a79052387bbbce18430d3ffadeb','8e177d4d82fa50f878397ee915f02e851491f7295460f83eee9450e3b0091ff5','8e177d4d82fa50f878397ee915f02e851491f7295460f83eee9450e3b0091ff5','6152f420a4c6a4d7b7fb6603662855579dec8f76e06d6844663b2507524d585d','f2fa637d0b3e518870979685ec43903ee9735ea40a2a1d9f17537735e27c9758','eef2946c43b40d0d75e502abe6ce73142fe1bb675a663b2b63fbccc63e6b5726','21be8f906a15d50043152b0d698e00eb3b0931f5b10b47c27056c682101a85b5']
if h in hash:
    print('good / هاتفك مصرح للدخول ')
    pass
else :
	while True:
	   print('your code is /', h)
	   print()
	   print('للتفعيل راسل المطور وادفع حق التحديث 1 usdt او 2k رشق وبعدها ارسله الكود يفعل لك ملاحضة لا تدور مجاني . ماراح ارد عليك')
	   time.sleep(90)
     
