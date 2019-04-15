# DB Maker 상품 모듈

## 상품등록하기

### DB Maker에 상품등록 요청

### 상품 페이지 자바스크립트파일 첨부

1) 아래 코드를 모든페이지 헤더부분에 추가해주세요.
```
<script src="link/to/be/decided.js"/>
<script>
  dbmaker.init('<제공된 제품 아이디를 String형태로 제공해주세요>');
</script>
```

2) 데이터가 생성되는 부분에 아래의 코드를 추가해주세요.
```
<script>
  dbmaker.record({
    name: String, 생성될 데이터 이름을 입력해주세요.
    phone: String, 생성될 데이터 전화번호를 입력해주세요.
    dob: String, 생성될 데이터 생년월일을 입력해주세요.
    sex: String, enum ['남', '여'], 성별을 String 형태로 입력해주세요. 옵션은 '남' 또는 '여'이며 이외데이터 입력시 랜덤으로 지정됩니다.
    availableTime: String, 상담가능시간을 String 형태로 입력해주세요.
    content: String, 위 필드를 벗어나는 항목을 String 형태로 입력해주세요. String 형태가 아닐경우 모든 요청들이 reject됩니다. 추가필드가 여럿 있을경우 '필드1: 필드1값, 필드2: 필드2값' 이런식으로 입력해주시면 됩니다.
  })
</script>
```

3) DB Maker에서 데이터가 잘 입력되는지, 어드민 대시보드가 잘 업데이트가 되는지 테스트 해보시고 문제가 있을경우 <DB Maker>로 연락주세요.
  
## 요청 반환값

### 반환값형태

- 모든 DB Maker 모듈 오청사항은 아래와같은 `JSON`형태의 반환값이 발생합니다.
```
{
  success: Boolean,
  message: String
}
```

- 사이트 자체적으로 에러핸들링을 하실때 `success` 값을 확인하시고 `false`일경우 에러핸들링을, `true`일경우 서브미션 확인을 해주시면됩니다. 모든 반환값은 `Promise`를 리턴해주며 IE등 하급 브라우저 타게팅시 [Promise Polyfill](https://github.com/stefanpenner/es6-promise)을 필수적으로 적용해주셔야합니다. 아래 예제를 참고하세요.
```
dbmaker.record({
  name: 'DB Maker',
  phone: '010123456789',
  dob: '1978.10.02'
  sex: '남',
  availableTime: '오전 1시',
  content: '최대한 빠르게 연락주세요.'
}).then(function(resp){
  if(resp.success){
    // 요청 성공시 할 작업
    // 예) window.alert('완료되었습니다.');
  }else{
    // 요청 실패시 할 작업
    // 예) window.alert('실패하였습니다.');
    // 추가적으로 success 값이 false일경우 resp.message에서 에러 메세지를 확인하실 수 있습니다. 에러메세지에대한 설명은 아래 에러 메세지 항목을 참고해주세요.
  }
})
```
