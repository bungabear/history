# 목차
* ## [ADB](#category-adb)
    * [패키지 목록 조회](#패키지-목록-조회)
    * [앱 덤프](#앱-덤프)
* ## 개발
    * [Bundle to String](#bundle을-string으로-만드는-함수)
    * [미디어 플레이어](#mediaplayer)
    * [화면 사이즈 가져오기](#화면-사이즈-가져오기)
    * [IntDef 정의하기](#intdef-정의하기)
    * [Service Handler Binder 차이](#handler와-binder차이)
    * [앱 디버그 상태 self 체크](#디버그-상태-체크)

* ### Bundle을 string으로 만드는 함수
  Bundle에서 **.keySet()** 으로 key목록을 받아 올 수 있고  
  **.get(key)** 로 Object타입의 value를 가져올 수 있다.
  ```java
  public String bundle2String(Bundle bundle){
    StringBuilder sb = new StringBuilder();
    Iterator<String> keys = bundle.keySet().iterator();
    while (keys.hasNext()){
        String key = keys.next();
        sb.append(key);
        sb.append(" : ");
        sb.append(bundle.get(key));
        if(keys.hasNext()){
            sb.append(", ");
        }
    }

    return sb.toString();
  }
  ```

* ### MediaPlayer

  * 미디어 플레이어는 datasouce 지정 후 prepare를 해야한다.   
  미디어가 큰경우 동기 prepare는 blocking이 발생하므로  
  **UI 스레드에서의 사용을 지양** 하고, **prepareAsync()** 와 **setOnPrepareListener()** 를 통해 비동기 작업을 하는것이 좋다.
    * 단, raw리소스는 MediaPlayer.create(context, R.raw.id)를 통해 prepare가 필요없다.

  * 미디어 객체는 prepare -> start -> stop -> prepare -> start로 동일한 미디어를 재사용 가능,  
  stop -> rest -> setDataSource로 재사용 가능하다.


* ### Asset 가져오기
  ```java
  getAsset().open("asset폴더내 경로")
  new Uri()
  ```

* ### 화면 사이즈 가져오기  
   ___Activity___
  ```java
  Display display = getWindowManager().getDefaultDisplay();  
  Point size = new Point();  
  display.getSize(size);  
  int width = size.x;  
  int height = size.y;  
  ```
  ___Serivce___

  ```java    
  WindowManager wm = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
  Display display = wm.getDefaultDisplay();  
  Point size = new Point();
  display.getSize(size);
  int width = size.x;
  int height = size.y;
  ```

* ### IntDef 정의하기
        
    디펜던시 추가
  ```java
    dependencies {  
      implementation 'com.android.support:support-annotations:23.4.0'  
    }
  ```

  구현 코드

  ```java
  static final int INITIALIZED = 0;  
  static final int STARTED = 1;  
  static final int ENDED = 2;  
  static final int CANCELED = 3;  

  @IntDef({INITIALIZED, STARTED, ENDED, CANCELED})  
  @Retention(RetentionPolicy.SOURCE)  
  @interface SharingState {}  
  ```
  
  
* ### Handler와 Binder차이
    1. 디버깅 용이성  
        Handler는 메세지전달형태여서 어느 위치에서 보낸 메세지가 문제인지 알 수 없다.  
        Binder는 함수를 직접 호출 하기때문에 errorstack에 표기된다

    2. 사용 용이성  
        Handler는 Static 함수로 사용할수 있도록 하면 어디서나 호출해서 보낼 수 있다.
        Binder는 매번 바인딩, 언바인딩을 해야하며 서비스가 죽었을경우 보장이 안된다.

* ### 디버그 상태 체크  
    가장 간단하게는 BuildConfig.DEBUG == true/false로 알 수 있지만, [정확하지 않다.](https://medium.com/@elye.project/checking-debug-build-the-right-way-d12da1098120)
    ```java
    boolean isDebug = ((getContext().getApplicationInfo().flags & ApplicationInfo.FLAG_DEBUGGABLE) != 0);
    ```
    이렇게 하면 된다.

* ### startActivity in Service

    서비스에서 startAcitivty를 할경우, FLAG_ACTIVITY_NEW_TASK를 추가해야한다.  
    ***FLAG_ACTIVITY_NEW_TASK*** 는 동일한 class의 인스턴가 이미 있으면 새로 실행 안하므로  
    서비스에서 새 인스턴스로 실행하고자 하면 ***FLAG_ACTIVITY_MULTIPLE_TASK*** 를 같이 추가해야한다.

## <a id="category-adb"/> ADB 
* ### 패키지 목록 조회

      pm list packages

    -f 옵션을 붙이면 경로도 나온다

* ### 앱 덤프

      pm dump [패키지명]

* ### 브로드캐스트 전체 조회

      dumpsys activity broadcasts // 전체 목록 조회
      dumpsys activity broadcasts history // 브로드캐스트 발생 기록 조회