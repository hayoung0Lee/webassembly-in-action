# webassembly-in-action
Follow webassembly in action


## 환경 설정
1. 가상환경이용해서(venv) python 3버전 설치하기(최소 2.7 이상이 필요) - [가상환경 관련 글](https://www.daleseo.com/python-venv/)
```
python3 -m venv .env
. .env/bin/activate
```

2. python3에 기본적으로 내장되어있는 로컬 웹서버를 이용
```
python -m http.server 8080
```

3. [emscripton 설치](https://emscripten.org/docs/getting_started/downloads.html)
```
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
./emsdk install 1.38.45
source ./emsdk_env.sh // 환경변수 설정, 캐쉬 안되기 때문에 따로 설정
```

- 환경변수 설정(https://life-of-panda.tistory.com/41)(https://elfinlas.tistory.com/266)
```
echo 'export PATH="$PATH:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk"' >> ~/.bash_profile

echo 'export PATH="$PATH:(your source ./emsdk_env.sh result)"' >> ~/.bash_profile

export PATH="$PATH:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk" // open .bash_profile



export PATH="$PATH:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/upstream/emscripten:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/node/12.18.1_64bit/bin:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/python/3.7.4-2_64bit/bin:/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk"

export EM_CACHE="/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/upstream/emscripten/cache"

export EMSDK_NODE="/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/node/12.18.1_64bit/bin/node"

export EMSDK_PYTHON="/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/python/3.7.4-2_64bit/bin/python3"

export SSL_CERT_FILE="/Users/hayoung/Desktop/Github Repos/webassembly-in-action/emsdk/python/3.7.4-2_64bit/lib/python3.7/site-packages/certifi/cacert.pem"


```
엠스크립튼 버전이 다르긴한데, 일단 쓰자. 이게 잘되야 #include <emscripten.h> 쓸수있다. 

4. Emiscripton and Node
나는 내 컴퓨터에 nvm 으로 node를 관리하고 있었는데, emiscripton 이 node를 또 가져오네.
[이거](https://github.com/emscripten-core/emscripten/issues/4848)이건 나와 같은 의문을 가졌던 분!

- nvm list 결과
<img src="./assets/1_nvm_list.png">
nvm은 node 14

- emsdk list 결과
<img src="./assets/2_emsdk_list.png">
emscripton은 12

잘모르겠으니 일단 넘어가자

5. wabt
https://github.com/WebAssembly/wabt#:~:text=WABT%20(we%20pronounce%20it%20%22wabbit,of%20tools%20for%20WebAssembly%2C%20including%3A&text=wasm%2Dinterp%3A%20decode%20and%20run,wat%2Ddesugar%3A%20parse%20.

이건 뭔가 사용하는건가본데, 아직 잘 모르겠다!


## 3장 웹어셈블리 모듈 만들어보기

- 엠스크립튼은 c/c++ 코드를 웹어셈블리 바이트코드로 컴파일하는 가장 검증된 툴킨!!. 원래는 저 코드를 asm.js로 바꿀려고 만들어진건데, 이제 웹어셈블리로도 컴파일된다!

- 엠스크립튼 모듈을 생성하는 세가지 방법: 
  - 엠스크립튼으로 웹어셈블리 모듈, 자바스크립트 연결 파일, html 템플릿 파일을 모두 생성
  - 엠스크립튼으로 웹어셈블리 모듈과 자바스크립트 연결파일 생성
  - 엠스크립튼으로 웹어셈블리 모듈 생성 

- 소수를 찾아 출력하는 프로그램 만들기
  1. c/c++ 코드로 소수를 찾아 출력하는 프로그램 만들기
  2. 엠스크립튼으로 웹어셈블리, html, 자바스크립트 파일을 생성
  3. 브라우저에서 html파일을 열어 실행 결과를 확인
  (맥에서 c++: https://csdiary.tistory.com/2)

- 3장 공부한 코드: https://github.com/hayoung0Lee/wasm-chapter-3



