# lunar_rust
日历、公历(阳历)、农历(阴历、老黄历)、佛历、道历，支持节假日、星座、儒略日、干支、生肖、节气、节日、彭祖百忌、每日宜忌、吉神宜趋凶煞宜忌、吉神(喜神/福神/财神/阳贵神/阴贵神)方位、胎神方位、冲煞、纳音、星宿、八字、五行、十神、建除十二值星、青龙名堂等十二神、黄道黑道日及吉凶等。lunar is a calendar library for Solar and Chinese Lunar. __This is a port from 6tail's https://github.com/6tail/lunar-python.__

## 示例
``` toml
[package]
name = "test_lunar_rust"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
lunar_rust = { path = "path/to/lunar_rust" }

```

``` rust
use lunar_rust::{lunar::{self, LunarRefHelper}, solar::{SolarRefHelper, self}};

fn main() {
    let lunar = lunar::from_ymd(1986, 4, 21);
    println!("{}", lunar.to_full_string());
    println!("--------");
    println!("{}", lunar.get_solar().to_full_string());
    
    println!("--------");

    let solar = solar::from_ymdhms(1957, 11, 1, 19, 20, 0);
    let lunar = solar.get_lunar();
    println!("{}", lunar.to_full_string());
    println!("--------");
    println!("{}", lunar.get_solar().to_full_string());
}

```

输出结果：
``` log
一九八六年四月廿一 丙寅(虎)年 癸巳(蛇)月 癸酉(鸡)日 子(鼠)时 纳音[炉中火 长流水 剑锋金 桑柘木] 星期四 北方玄武 星宿[斗木獬](吉) 彭祖百忌[癸不词讼理弱敌强 酉不会客醉坐颠狂] 喜神方位[巽](东南) 阳贵神方位[巽](东南) 阴贵神方位[震](正东) 福神方 位[艮](东北) 财神方位[离](正南) 冲[(丁卯)兔] 煞[东]
--------
1986-05-29 00:00:00 星期四 (国际维和人员日) 双子座
--------
一九五七年九月初十 丁酉(鸡)年 庚戌(狗)月 丁丑(牛)日 戌(狗)时 纳音[山下火 钗钏金 涧下水 钗钏金] 星期五 西方白虎 星宿[娄金狗](吉) 彭祖百忌[丁不剃头头必生疮 丑不冠带主不还乡] 喜神方位[离](正南) 阳贵神方位[乾](西北) 阴贵神方位[兑](正西) 福神方 位[巽](东南) 财神方位[坤](西南) 冲[(辛未)羊] 煞[东]
--------
1957-11-01 19:20:00 星期五 (万圣节) 天蝎座
```
详细运用方案，请查阅 `tests` 及 6tail 的文档.

## 文档
请移步至 https://6tail.cn/calendar/api.html

## 节假日
```rust
use lunar_rust::{
    holiday::{self, HolidayRefHelper},
    lunar::{self, LunarRefHelper},
    solar::{self, SolarRefHelper},
    util::holiday_util::{self, HolidayUtilRefHelper},
};
fn main() {
    let solar = solar::from_ymd(2025, 5, 5);
    let lunar = solar.get_lunar();
    // 初八
    println!("今天的中文：{}", lunar.get_day_in_chinese());

    println!("农历全部字符串：{}", lunar.to_full_string());
    println!("--------");
    println!("阳历全部字符串：{}", lunar.get_solar().to_full_string());
    println!("--------");
    let holiday = holiday_util::get()
        .get_holiday(2025, Some(5), Some(5))
        .unwrap();
    println!("假日名字：{}", holiday.get_name());
    println!("是否上班：{}", holiday.is_work());
}
初八
二〇二五年四月初八 乙巳(蛇)年 辛巳(蛇)月 甲戌(狗)日 子(鼠)时 纳音[覆灯火 白蜡金 山头火 海中金] 星期一 [立夏] 东方青龙 星宿[心月狐](凶) 彭祖百忌[甲不开仓财物耗散 戌不吃犬作怪上床] 喜神方位[艮](东北) 阳贵神方 位[坤](西南) 阴贵神方位[艮](东北) 福神方位[坎](正北) 财神方位[艮](东北) 冲[(戊辰)龙] 煞[北]
--------
2025-05-05 00:00:00 星期一 (马克思诞辰纪念日) 金牛座
--------
劳动节
false
```


## Note:
As this is just a port, I do not claim credit for any originality of the work.