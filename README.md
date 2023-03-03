# RazerBladeAdvance2021HackintoshEFI
**硬件配置**  
CPU：i7 10875H  
硬盘：WD SN750 2T  
WI-FI：AX201 网卡  
显卡：RTX3080 8G  
内存：64G DDR4 3200  
显示器：1080P 300赫兹刷新率  

**OpenCore 版本**  
0.6.4  

**Mac OS 版本**  
Mac Monterey

**正常运行功能**  
wifi   正常  
蓝牙    正常  
触摸板  正常  
usb    正常
显示    正常（安装betterDisplay 出发hidpi)
usb    正常    
CPU睿频 正常    
耳机    正常    
音响    正常    
休眠    正常      
typec 充电 正常    
接力    正常    

**无法使用功能**  
独立显卡      无法使用    
hdmi        无法使用    
typec显示    无法使用    
airdrop     无法使用（很有意思的是，如果你是安卓手机，可以google play安装anddrop软件， 但手机和笔记本在同一局域网内，就可以实现和白苹果一摸一样的airdrop功能了，实在是让人无语）      
随航         无法使用（可能是apple id问题，我的白苹果+iPad 同样无法使用） 

**使用小tips** 
1. 如何双屏显示  
购买一个支持displaylink协议的拓展坞，我在咸鱼购买的hp traval dock（200元）  
macos 安装DisplayLink 软件 即可实现链接外部显示器
2. 键盘键位不适应怎么办？   
安装Karabiner-elements  
Simple Modifications 中 将left control 和left command 键位功能互换  
Complex Modifications 中下载网上别人写好的脚本，如下3个  
   - Change Command+tab to control+tab (实现alt+tab 切换app功能)  
   - Bind Option+tab to command+tab (实现control+tab 同一app切换标签页功能)  
   - Use left shift to change to/from English input (点击shift 切换自带输入法 中英文输入)  
3. 鼠标不好用怎么办？  
安装Mac Mouse fix 软件， 实现浏览网页平滑滚动，同时可以自定义鼠标其他按键功能，十分好用  
4. 别忘记打开3指拖拽功能    
在触摸板设置中并没有打开该功能的开关，需要在 "辅助功能"-"指针控制" 中启用  
5. 链接windows 虚拟机后键位不对如何解决  
使用Karabiner-elements替换了键盘键位之后，如果使用微软的"Remote Desktop" 链接到windows虚拟机  
会发现在windows 虚拟机中键位就错乱了。 使用Hammerspoon 写了一个自动切换脚本， 判断如果当前是Remote Desktop 程序被激活 就不让 Karabiner-elements 切换键位  
6. 















