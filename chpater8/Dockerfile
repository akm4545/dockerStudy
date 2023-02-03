#기반 이미지
FROM diamol/node

#메모리 체크에 사용될 환경벼수
ENV MAX_ALLOCATION_MB=4096  \
    LOOP_ALLOCATION_MB=512 \
    LOOP_INTERVAL_MS=2000

#memory-check.js에 헬스체크 로직이 있음
#정상적인 값을 return 하면 && 뒤의 명령을 수행
#즉 메모리가 정상이면 실행
CMD node memory-check.js && \
	node momery-hog.js

#5초 간격으로 헬스체크를 수행한다
HEALTHCHECK --interval=5s \
	CMD node memory-check.js

WORKDIR /app
COPY src/ .