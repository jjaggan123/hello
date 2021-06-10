포아송 분포
just another rep



#포아송 분포 심화
포아송 분포(Poisson distribution)는 일정한 단위 시간, 단위 공간에서 어떤 사건이 랜덤하게 발생하는 경우에 사용할 수 있는 이산형 확률분포입니다.가령, 1시간 동안 은행에 방문하는 고객의 수, 1시간 동안 콜센터로 걸려오는 전화의 수, 1달 동안 경부고속도로에서 교통사고가 발생하는 건수,
포아송 분포에서 모수 λ (lambda 라고 발음함)는 일정한 단위 시간 또는 단위 공간에서 랜덤하게 발생하는 사건의 평균 횟수를 의미합니다
  밀도 함수
 d
  dpois(x, lambda)
  누적 분포 함수
 p
  ppois(q, lambda, lower.tail = TRUE/FALSE
  분위수 함수
 q
  qpois(p, lambda, lower.tail = TRUE/FALSE
  난수 발생
 r
  rpois(n, lambda)


P ( X = 15) 확률 계산 : dpois(x, lambda)
문제)  어느 은행의 1시간 당 방문 고객 수가 λ = 20 인 포아송 분포를 따른다고 한다.  그럼 1시간 당 방문고객수가 15명일 확률은?

P ( X <= 15) 확률 계산 : ppois(q, lambda, lower.tail = TRUE)
문제)  어느 은행의 1시간 당 방문 고객 수가 λ = 20 인 포아송 분포를 따른다고 한다.  그럼 1시간 당 방문고객수가 15명 이하일 확률은?

특정 확률 값에 해당하는 분위수 계산 : qpois(p, lambda, lower.tail=TRUE)
문제) 어느 은행의 1시간 당 방문 고객 수가 λ = 20 인 포아송 분포를 따른다고 한다.  만약 1시간 동안 방문한 고객수에 해당하는 확률이 15.65131% 이라면 이는 몇 명에 해당하는가?

난수 발생 : rpois(n, lambda)
문제 ) λ = 20 인 포아송 분포에서 n = 1000 개의 난수를 발생시키고, 도수분포표를 구하고, 도수별 막대그래프를 그려보아라.
rpois(n=1000, lambda = 20)
table(rpois(n=1000, lambda = 20))
plot(table(rpois(n=1000, lambda = 20)))
위 그래프를 보면 λ = 20 이므로 평균이 20 인 위치에서 가장 높게 모여있고, 오른쪽으로 꼬리가 긴 포아송 분포를 따르고 있음을 알 수 있습니다.
빈도 데이터 분석을 위한 포아송 회귀모델(Poisson Regression Model)과 과대산포, 과대영 문제가 있을 경우 대안으로 활용할 수 있는 모델에 대한 내용은 https://rfriend.tistory.com/490 를 참고하세요. 

람다 값이 커질수록 정규분포 모형에 가까워진다-실습
pois1 <- rpois(n=10000, lambda = 1 )
pois2 <- rpois(n=10000, lambda = 2 )
pois3 <- rpois(n=10000, lambda = 5 )
pois4 <- rpois(n=10000, lambda = 10 )
pois5 <- rpois(n=10000, lambda = 20 )
pois <- data.frame(Lamda1=pois1, Lamda2=pois2, Lamda5=pois3, Lamda10=pois4, Lamda20=pois5)
#plot하기 쉽도록 녹이기 위해서 reshape를 불러온다
library(reshape)

#새로운 열 이름을 정돈하기 위해 stringr패키지 로딩
pois <- melt(data = pois, variable_name = "Lamda", value.name= "X")
library(stringr)
pois$Lamda <- as.factor(as.numeric(str_extract(string = pois$Lamda, pattern = "\\d+")))
head(pois)
tail(pois)

library(ggplot2)
ggplot(pois, aes(x=X))+geom_histogram(binwidth = 1)+facet_wrap(~Lamda)+ggtitle("Probability Mass Function")


