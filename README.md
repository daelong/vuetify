https://www.openbrewerydb.org/documentation/01-listbreweries에 있는 https://api.openbrewerydb.org/breweries api를 호출하여 데이터 표시
exam1 : 
1. <ul><li></li></ul> 태그를 사용하여 카드형으로 리스트 아이템 표시
2. 아이템에 표시할 내용은 name, brewery_type, country, website_url 표시
3. 카드 상단에는 닫기 버튼이 있어서 버튼을 누르면 해당 아이템 가리기 또는 사라지게 하기

exam2 :
1. exam 1의 1과 동일
2. exam 1의 2와 동일
3. 카드 상단에는 닫기 대신 접기 버튼으로 아이템 접기
4. 스크롤 다운하여 하단에 다다랐을 때 추가적인 브루어리 리스트 가져와서 표시하기 (infinite scroll)

exam3 : 
1. <table> 태그를 사용하여 테이블 형식으로 아이템 표시
2. 아이템에 표시할 column 내용 name, brewery_type, country, website_url 표시
3. table row를 클릭하면 상세 정보 표시
  -> 표시할 필드: name, brewery_type, country, state, city, phone, website_url
  -> 상세정보 표시는 선택한 row 하단에 확장
4. 여러 페이지 및 추가 아이템 표시는 infinite 스크롤 (기본 per_page=50)
 
exam4 : 
1. 문제 3의 1번과 동일, row 별로 배색처리 (흰색 #fff, 회색 #eee, 흰색, 회색 ... 반복)
2. 문제 3의 2번과 동일, row 의 가장 좌측에 순번 ordering column을 추가하여 표시
3. 문제 3의 3번과 동일, 카드 모양의 modal 형태로 표시
4. 테이블 하단에 pagination 버튼 추가 및 표시, per_page 값은 10으로 고정 페이지 번호는 1 ~ 10 까지만 고정으로 표시 그 이상은 표시하지 않아도 됨
이전, 이후(1 페이지 증감)와 페이지 번호 형태로 표시
< 1 2 3 4 5 6 7 8 9 10 >

exam5 : 
1. 문제 4와 동일
2. 문제 4와 동일
3. 문제 4와 동일
4. 문제 4와 동일
5. 테이블 헤더 영역의 colmn 클릭 시 오름/내림차순 정렬 표시
정렬 유형 :
정렬 하지 않음 (API 호출 시 반환된 데이터 순서대로 표시), 오름차순, 내림차순
동일 column 클릭 시 위 3가지 상태가 순차적으로 변경
sort 참고
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

exam6 : 
1. 문제 4와 동일
2. 문제 4와 동일
3. 문제 4와 동일
4. pagination은 표시하지 않고 페이지 1번만 표시
5. 문제 5와 동일
6. Add 기능 추가
API를 통해 호출되는 원격 리포지터리의 수정 권한이 없으므로, 이미 수신된 로컬 데이터를 대상으로 함
입력 받을 필드 :
필수와 선택 필드 구분 됨(필수 필드 값은 null 또는 undefined 이거나 공백 문자가 아니어야 함)
필수 - name, brewery_type
선택 - country, state, city, phone, website_url
brewery_type, country 필드는 input이 아닌 select 태그(일명 콤보박스)를 이용하여 입력
brewery_type 및 country 선택 아이템 적용을 위한 참고사항
brewery_type : micro, contract, brewpub, regional, planning, proprietor
country는 하단에 명시된 json 값을 이용
https://gist.github.com/keeguon/2310008

exam7: 
1. edit 기능 추가
2. Delete 기능 추가

