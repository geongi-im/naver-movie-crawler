# naver-movie-crawler
네이버 영화 정보 및 사용자 평점 수집기
1. 영화 정보 수집(movie collection)
 - 관객 많은순, 랭킹 높은순, 평점 높은순 등 특정 영화군 데이터 수집
 - 약 1000개의 영화 데이터 수집
 - <영화키, 영화제목 등 영화주요정보> 
   - 영화주요정보 : 영화세부페이지안에 개요, 러닝타임, 개봉일, 감독, 출연진, 등급(국내/해외)
 - 영화평점을 업데이트 시켜주기위해서 마지막평점남긴사람번호를 기록함.
 
2. 영화 평점 수집(score_movie key collection)
 - (1)에서 수집된 영화들을 기준으로 해당 영화 내부의 유저들의 평점을 수집함
 - 영화의 총 평점 갯수가 얼마인지 체크함. (모든 평점을 다 가져올때 데이터가 얼마나 될까? 서버부하는 괜찮을까?)
 - 처음에는 100개만 가져오는걸로 limit parameter 활용함
 - (중복된 평점이 들어가지않게 방지 할방법 생각) => 영화 평점에 번호가 있음. 해당 번호를 기준으로 큰것만 삽입하게함.
 - <유저키, 별점, 영화평, 날짜>
 
3. 유저 기준 평점 수집(user_user key collection)
 - (2)에서 수집된 영화 평점을 남긴 유저키를 기준으로 유저들에 대한 평점 정보를 수집함
 - 해당 유저키의 collection이 있는지 조회함. collection이 없다면 user key의 collection 생성, 있으면 continue (앞으로 유저들이 계속 평을 남길거니까 모든 유저의 컬렉션 만듬)
 - (유저도 중복 평점이 발생할수있어서, 해당 유저가 마지막으로 남긴 번호보다 큰값만 삽입해야함) => movie collection 처럼 user collection도 필요한가? 아는정보가 없을텐데... 
 - <영화키, 영화제목, 별점, 영화평, 날짜>
