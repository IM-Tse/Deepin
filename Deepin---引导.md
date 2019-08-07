## 1. 将Windows放到第一个启动项

```
sudo mv /etc/grub.d/30_os-prober /etc/grub.d/08_os-prober 

sudo update-grub
```

