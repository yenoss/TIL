# ElasticLoadBalance

## WHAT?
+ ElasticLoadBalance 적용기.

## 1. ElasticLoadBalance
+ ELB는 서버의 부하를 분산해주는 aws 자원이다. 분산할 서버를 골라서 부하 분산을 할수도 있고 autoScaling과 함께라면 서버의 요청이 많아 부하가 걸릴때에 서버를 자동으로 늘려 서비스를 안정화 시켜주는 역할을 한다.
+ ELB + Auto Scaling 설정에 대해 대략적으로 정리해본다.

#### LoadBalancers
+ aws 이전에 lb에는 하드웨어적으로  l4/7 스위치로 사용하나 가격 및 유지 설비등의 문제로 소프트웨어적 lb를 많이 사용되었다(nginx,apache). 
+ 마찬가지의 역할로 부하분산을 위한 lb를 aws에서 제공해 준다. 

aws에서 lb를 만들고 + target group을 만듬, targetgroup이 실제 서버들이 붙는 그룹을 의미함. 후에  autoscaling옵션에 해당 타겟그룹을  설정해주면 그 그룹에 추가된 서버들이 붙게된다.

autosclaing에서는 첫째로 launchconfiguration을 추가 서버가 뜰때 어떠한 환경으로 혹은 시작 스크립트는 어떻게 떠야하며, securitygroup의 설정 등을 하게된다.

autoscaling그룹에서는 launchconfiguration을 기반으로 서버가 어떠한 환경에서 (cpu..)떠야하는지 뜬 서버는 어느 로드밸런서에 붙어야하는지에 대한 설정을한다.




## REF.