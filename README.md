# <div align="center">리싸이클러뷰_2</div>

## <div align="center">👋🏻 처음 화면 👋🏻</div>
### 검색창과 리싸이클러뷰 2개가 있다.
![스크린샷 2022-10-15 오후 11 48 37](https://user-images.githubusercontent.com/102125786/195992738-1e9fe3c2-4cde-4b17-accb-51ab42b3ea19.png)

## <div align="center">📱 어플 설명 📱</div>
### 처음 보이는 가로로된 리싸이클러뷰가 보인다.
![스크린샷 2022-10-15 오후 11 54 08](https://user-images.githubusercontent.com/102125786/195992969-06b9adaf-1e91-4fa9-9e0b-4f7e50d0aa25.png)

### 위에 검색창에 보고싶은 책 이름을 검색한다.
![스크린샷 2022-10-15 오후 11 55 23](https://user-images.githubusercontent.com/102125786/195993027-8315ee05-a034-470c-8693-d4b8ff32cb8a.png)

### 결과가 리싸이클러뷰로 나온다.
![스크린샷 2022-10-15 오후 11 56 31](https://user-images.githubusercontent.com/102125786/195993091-9a1fb928-e9fe-496f-997b-3ac6576d23cd.png)

## <div align="center"> ✍🏻 중요한 내용 ✍🏻 </div>
### 검색하는 코드와 api 코드
```kotlin
  binding.etSearch.addTextChangedListener{
			val retrofitNaver = Retrofit.Builder()
				.baseUrl("https://openapi.naver.com")
				.addConverterFactory(GsonConverterFactory.create())
				.build()
			val bookNaverApi = retrofitNaver.create(BookNaverAPI::class.java)
			bookNaverApi.getBooksByName(
				"yFA9VJu4JIxrg_6ODIU4", //getString(R.string.naver_id),
				"otq3y_P8ZB", //getString(R.string.naver_secret_key),
				binding.etSearch.text.toString()
			).enqueue(object : Callback<SearchBookNaverDTO> {
				override fun onResponse(
					call: Call<SearchBookNaverDTO>,
					response: Response<SearchBookNaverDTO>
				) {
					response.body()?.let {
						it.books.forEach { book ->
							// 리싸이클러뷰에서 사용할 리스트를 저장해줍니다.
							adapterNaver.submitList(it.books)
						}
					}
				}

				override fun onFailure(call: Call<SearchBookNaverDTO>, t: Throwable) {
				}
			})
		}
```

## <div align="center"> 😅 미흡한 부분 😅 </div>
### 아직 api에 대한 활용이 부족하며 더 많은 기능이 들어가지 못함...
