FROM diamol/golang AS golang 기반 이미지

COPY main.go . 기반 이미지에서 생성 이미지로 복사
RUN go build -o /web/server 생성 이미지의 해당 경로에 빌드
RUN chmod +x /web/server 디렉토리에 권한 부여

ENV USER=sixeyed 환경변수 세팅
EXPOSE 80 가동 포트
CMD ["/web/server"] 실행

//빌드 이미지에서 어떻게 가져오는지 모르겠음 

WORKDIR web 작업 디렉토리 생성
COPY index.html . 기반 이미지에서 

일곱단계를 수행해야 함

답안 
//제일 용량을 많이 차지하고 오래 걸리면서 자주 바뀌지 않으므로 먼저 실행하는듯함
//빌드에 관련된 파일들이 있는 기반 이미지
FROM diamol/golang AS builder

//파일 복사
COPY main.go .
//빌드
RUN go build -o /server
//권한 부여
RUN chmod +x /server

# app
//위의 빌드 단계와 분리함으로써 빌드단계를 제외시켜 용량을 경량화 시킨다
//인덱스 html 이 들어있는 이미지
FROM diamol/base

//80번 포트 사용
EXPOSE 80
//실행
CMD ["/web/server"]
//환경변수
ENV USER="sixeyed"

//디렉토리 생성
WORKDIR web
//빌드 스테이지의 작업물 복사
COPY --from=builder /server .
//인덱스 파일 복사
COPY index.html .
