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
    
