* 화면 사이즈 가져오기  
    ___Activity___

      Display display = getWindowManager().getDefaultDisplay();  
      Point size = new Point();  
      display.getSize(size);  
      int width = size.x;  
      int height = size.y;  

    ___Serivce___
    
      WindowManager wm = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);  
      Display display = wm.getDefaultDisplay();  
      Point size = new Point();
      display.getSize(size);
      int width = size.x;
      int height = size.y;

* IntDef 정의하기
        
    디펜던시 추가

      dependencies {  
        implementation 'com.android.support:support-annotations:23.4.0'  
      }

    구현 코드

      static final int INITIALIZED = 0;  
      static final int STARTED = 1;  
      static final int ENDED = 2;  
      static final int CANCELED = 3;  

      @IntDef({INITIALIZED, STARTED, ENDED, CANCELED})  
      @Retention(RetentionPolicy.SOURCE)  
      @interface SharingState {}  
  
  
* Handler와 Binder차이
    1. 디버깅 용이성  
        Handler는 메세지전달형태여서 어느 위치에서 보낸 메세지가 문제인지 알 수 없다.  
        Binder는 함수를 직접 호출 하기때문에 errorstack에 표기된다

    2. 사용 용이성  
        Handler는 Static 함수로 사용할수 있도록 하면 어디서나 호출해서 보낼 수 있다.
        Binder는 매번 바인딩, 언바인딩을 해야하며 서비스가 죽었을경우 보장이 안된다.

* 디버그 상태 체크  
    가장 간단하게는 BuildConfig.DEBUG == true/false로 알 수 있지만, [정확하지 않다.](https://medium.com/@elye.project/checking-debug-build-the-right-way-d12da1098120)
    
      boolean isDebug = ((getContext().getApplicationInfo().flags &  ApplicationInfo.FLAG_DEBUGGABLE) != 0);

    이렇게 하면 된다.