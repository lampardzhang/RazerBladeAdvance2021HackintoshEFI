# RazerBladeAdvance2021HackintoshEFI



**硬件配置**  
CPU：i7 10875H  
硬盘：WD SN750 2T  
WI-FI：AX201 网卡  
显卡：RTX3080 8G  
内存：64G DDR4 3200  
显示器：1080P 300赫兹刷新率    

**下图为具体版本信息**   

![](https://raw.githubusercontent.com/lampardzhang/imagesForUpgit/master/2023/03/upgit_20230307_1678183502.png)



**OpenCore 版本**  
0.6.4     


**Mac OS 版本**  
Mac Monterey

**正常运行功能**  
wifi   正常  
蓝牙    正常  
触摸板  正常  
usb    正常
显示    正常（安装betterDisplay 触发hidpi)
usb    正常    
CPU睿频 正常    
耳机    正常    
音响    正常    
休眠    正常      
typec 充电 正常    
接力    正常 
电池    正常充放电，大概可以使用4小时多一点， 比windows使用时间少了2个小时左右
不知道原因

**无法使用功能**  
独立显卡      无法使用    
hdmi        无法使用    
typec显示    无法使用    
airdrop     无法使用（很有意思的是，如果你是安卓手机，可以google play安装anddrop软件， 但手机和笔记本在同一局域网内，就可以实现和白苹果一摸一样的airdrop功能了，实在是让人无语）      
随航         无法使用（可能是apple id问题，我的白苹果+iPad 同样无法使用）   
屏幕亮度自动响应  无法使用， 不过这个我在windows也无法使用， 硬件就不支持    
屏幕亮度记录功能  无法使用   手动调节屏幕亮度之后，休眠之后屏幕亮度又变回默认值（70%）  

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
会发现在windows 虚拟机中键位就错乱了。 使用"Hammerspoon"写了一个自动切换脚本， 判断如果当前是Remote Desktop 程序被激活 就不让 Karabiner-elements 切换键位  
```
if hs.fs.attributes("Spoons/Knu.spoon") == nil then
  hs.execute("mkdir -p Spoons; curl -L https://github.com/knu/Knu.Spoon/raw/release/Spoons/Knu.spoon.zip | tar xf - -C Spoons/")
end
knu = require("knu")
-- Function to guard a given object from GC
guard = knu.runtime.guard

-- Enable auto-restart when any of the *.lua files under ~/.hammerspoon/ is modified
knu.runtime.autorestart(true)

-- Switch between Karabiner-Elements profiles by keyboard

function switchKarabinerElementsProfile(name)
  hs.execute(knu.utils.shelljoin(
      "/Library/Application Support/org.pqrs/Karabiner-Elements/bin/karabiner_cli",
      "--select-profile",
      name
  ))
end

function applicationWatcher(appName, eventType, appObject)
    print("appName is  "..(appName))
    print("eventType is  "..(eventType))
    if (eventType == hs.application.watcher.activated) then
        if (appName == "Microsoft Remote Desktop") then
            switchKarabinerElementsProfile("R")
        end
    end
    if (eventType == hs.application.watcher.deactivated) then
        if (appName == "Microsoft Remote Desktop") then
            switchKarabinerElementsProfile("N")
        end
    end
end
appWatcher = hs.application.watcher.new(applicationWatcher)
appWatcher:start()
```
6. 屏幕亮度记录功能实现  
   同样使用Hammerspoon 写脚本，记录休眠前的屏幕亮度， 唤醒后 set 屏幕亮度为前面记录值  
   
   ```
   local lastBrightness  
      function systemWakeUpCallback(eventType)  
         if(eventType==hs.caffeinate.watcher.screensDidWake) then  
            print("system previous brightness is "..(lastBrightness))  
            hs.brightness.set(lastBrightness)  
         end
         if(eventType==hs.caffeinate.watcher.screensDidSleep) then  
            lastBrightness = hs.brightness.get()  
            print("set previous brightness is "..(lastBrightness))  
         end  
      end  
      wakeUpWatcher = hs.caffeinate.watcher.new(systemWakeUpCallback)  
      wakeUpWatcher:start()  
   ```
   
7. 其余待办:        
   
      1. 为了测试sidebar功能, 需要换一个无线网卡.  
   2. 目前修改host 内容为如下：  
      140.82.113.3    github.com  
      185.199.108.153 assets-cdn.github.com  
      199.232.69.194  github.global.ssl.fastly.net     
   3. 使用 
   ```
      dscacheutil -flushcache
   ```
   



![截屏2023-03-09 16.27.49](https://raw.githubusercontent.com/lampardzhang/imagesForUpgit/master/2023/03/upgit_20230309_1678350492.png)

















