![alt text](image-1.png)
---

웹뷰 사이드바 > 앱뷰 호출 로직

- 사이드바 js에 음성방송 전용 호출 함수 생성
```js
 if (hasActualSubMenu) {
                      menuHtml += '<li class="has-submenu">';
                      menuHtml += '<button class="submenu-toggle">' + menuList[i].groupName + '</button>';
                  } else {
                      // 하위 메뉴가 없는 상위 메뉴 (ID 49 체크)
                      if (menuList[i].id == 49) {
                          menuHtml += '<li><a href="javascript:void(0);" onclick="openAndroidVoiceMenu()">' + menuList[i].groupName + '</a></li>';
                      } else if (menuList[i].id == 16) {
                            menuHtml += '<li><a href="javascript:void(0);" onclick="openResidentManage()">' + menuList[i].groupName + '</a></li>';
                      } else {
                          menuHtml += '<li><a href="' + menuList[i].menuPath + '?idx=' + highIdx + '00">' + menuList[i].groupName + '</a></li>';
                      }
                  }

                  // 하위 메뉴 루프
                  let subMenuHtml = '';
                  let subMenuIndex = 1;
                  $.each(menuList, function(j) {
                      if (menuNo === menuList[j].parentId && menuList[j].menuLevel === 1) {
                          let lowIdx = String(subMenuIndex).padStart(2, '0');
                          let currentMenu = menuList[j];
                          if (subMenuIndex === 1) subMenuHtml += '<ul class="submenu">';

                          if (currentMenu.id == 49) {
                              subMenuHtml += '<li><a href="javascript:void(0);" onclick="openAndroidVoiceMenu()">' + currentMenu.groupName + '</a></li>';
                          } else if (menuList[i].id == 16) {
                                menuHtml += '<li><a href="javascript:void(0);" onclick="openResidentManage()">' + menuList[i].groupName + '</a></li>';
                          } else {
                              subMenuHtml += '<li><a href="' + currentMenu.menuPath + '?idx=' + highIdx + lowIdx + '">' + currentMenu.groupName + '</a></li>';
                          }
                          subMenuIndex++;
                      }
                  });

// 안드로이드 인터페이스 호출 함수
function openAndroidVoiceMenu() {
    if (window.android && window.android.openNativeScreen) {
        window.android.openNativeScreen('voiceSend');
    } else if (window.Android && window.Android.openNativeScreen) {
        window.Android.openNativeScreen('voiceSend');
    }
}
```

- 안드로이드 코틀린 서비스에서 케이스 추가
```java
@JavascriptInterface
        fun openNativeScreen(screenType: String) {
            activityRef.get()?.let { activity ->
                activity.runOnUiThread {
                    when (screenType) {
                        "userInfoAdd" -> {
                            val intent = Intent(activity, UserInfoAddActivity::class.java)
                            activity.startActivity(intent)
                        }
                        "voiceSend" -> { // [추가] 음성방송 케이스 추가
                            val intent = Intent(activity, VoiceBroadcastActivity::class.java)
                            activity.startActivity(intent)
                        }
                        // 다른 화면 추가 가능
                    }
                }
            }
        }
```
---
- 헤더 / 사이드바 보이게 수정

- 주소록 카드
    - [✔️] 탭 별 주소록 그룹 출력
        - [✔️] 각 주소록 그룹 별 주민정보 테이블로 보이게 수정
    - [✔️] 검색 필터 기능
    - [✔️] 주소록 선택 기능

- 추가 발송대상
    - [✔️] 직접입력 선택 시 입력 창 출력
        - [✔️] 검색 필터링 기능
    - [✔️] 양식 다운로드
    - [✔️] 액셀 업로드
    - [✔️] 초기화

- 음성 발송(VMS)
    - [✔️] 회선번호 조회
    - [✔️] 음성 녹음 기능
        - [✔️] 녹음 파일 저장
        - 음성녹음 미리듣기 기능
    - 녹음 파일 첨부 기능
    - 예약 발송 체크
    - 메시지 북마크 조회
    - 전송 기능