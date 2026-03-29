### 개인정보 제공동의 APP 개발📱
![alt text](image-1.png)
#### 화면 구현
상단 : 탭 선택 > 주소록 그룹 출력 및 선택 > 추가 발송 대상[선택] 

하단 : 회신번호 조회 > 발송 타이틀 입력 > 음성 녹음 카드 > STT 변환 텍스트 > 녹음 파일 첨부[선택] > 메시지 북마크

- activity_voice_broadcast.xml
```xml
 <androidx.recyclerview.widget.RecyclerView
    android:id="@+id/rv_address_list"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:overScrollMode="never"
    app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager"
    tools:listitem="@layout/item_address_node" />
```

- item_address_node.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="44dp"
        android:gravity="center_vertical"
        android:orientation="horizontal"
        android:paddingHorizontal="4dp"
        android:background="?attr/selectableItemBackground">

    <ImageView
            android:id="@+id/iv_icon"
            android:layout_width="22dp"
            android:layout_height="22dp"
            android:src="@drawable/ic_folder"
            app:tint="#B0B8C1"
            android:layout_marginEnd="10dp" />

    <TextView
            android:id="@+id/tv_group_name"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="그룹 이름"
            android:textSize="14sp"
            android:textColor="#4E5968" />
</LinearLayout>
```
- 백엔드 연동을 위한 로직 구조
```java
// 예시: 탭 클릭 시 리스트 갱신 로직
tabStaff.setOnClickListener(v -> {
    updateTabUI(tabStaff); // UI 강조 변경
    fetchAddressData("STAFF"); // 백엔드 호출 (직원 데이터 요청)
});

tabPersonal.setOnClickListener(v -> {
    updateTabUI(tabPersonal);
    fetchAddressData("PERSONAL"); // 백엔드 호출 (개인 데이터 요청)
});
```