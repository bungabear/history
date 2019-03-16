# 안드로이드 사용 팁

* 안드로이드 파이(9.0)이후의 화면회전 버튼 없애기  
  <img src="https://user-images.githubusercontent.com/22841704/54477216-198d1680-4849-11e9-99ef-130ff491d518.jpg" width=200/>
  
      adb shell settings put secure show_rotation_suggestions 0  
  0은 비활성화 1은 활성화이며, 기기를 재부팅해야 적용됨.