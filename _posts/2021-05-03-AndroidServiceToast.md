1. 안드로이드 서비스 스레드 안에서 토스트 사용
- Thread에서 Toast 직접 사용 불가
- 보통 Thread에서 사용 하는 MainActivity.this.runOnUiThread()도 Service에서는 사용 불가
- Handler를 사용하여 처리
- 서비스 클래스 안에서 멤버 변수 선언
    - Handler handler;
    - onCreate() 내부에서 초기화
    - handler = new Handler();
    - 함수 추가
    - private void _runOnUiTHread(Runnable runnable) {
        handler.post(runnable);
    }
    - 원하는 토스트 띄우기
    - _runOnUiThread(new Runnable() {
        public void run() {
            Thoast.makeText(getApplicationContext(), "Message", Toast.LENGTH_LONG).show();
        }
    });

    