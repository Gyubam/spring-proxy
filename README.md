## 프록시 디자인 패턴 적용

요구사항 - 기존 클래스의 원본 코드를 수정하지 않고 LogTrace 기능 추가

- app
  - v1 - 인터페이스 및 구현 클래스의 스프링 빈 수동 등록
  - v2 - 구체 클래스의 스프링 빈 수동 등록
  - v3 - 컴포넌트 스캔 통한 스프링 빈 자동 등록

</br>

- config
  - v1_proxy
    - interface_proxy - 인터페이스 기반 프록시 구현
    - concrete_proxy - 구체 클래스 기반 프록시 구현

  - v2_dynamicproxy
    - LogTraceBasicHandler - JDK 동적 프록시 적용
    - LogTraceFilterHandler - JDK 동적 프록시 적용 + 메서드 필터 기능
  
  - v3_proxyfactory
    - advice
      - LogTraceAdvice - 어드바이스 구현 코드
    - ProxyFactoryConfigV1 - V1(인터페이스 기반)에 프록시 팩토리 적용
    - ProxyFactoryConfigV2 - V1(구체 클래스 기반)에 프록시 팩토리 적용
    
  - v4_postprocessor
    - postprocessor
      - PackageLogTracePostProcessor - BeanPostProcessor 클래스 구현
    - BeanPostProcessorConfig - V1, V2, V3 빈 후처리기 적용
    
  - v5_autoproxy
    - AutoProxyConfig - AnnotationAwareAspectJAutoProxyCreator 통한 프록시 생성 자동화
    
  - v6_aop
    - aspect
      - LogTraceAspect - @Aspect 프록시 적용
</br>
</br>


- test
  - pureproxy
    - proxy - 프록시 패턴 예시 Test 코드
    - decorator - 데코레이터 패턴 예시 Test 코드
    - concreteproxy - 구체 클래스 기반 프록시 Test 코드
  - jdkdynamic - JDK 동적 프록시 Test 코드 (인터페이스가 있는 경우)
  - cglib - CGLIB 통한 동적 프록시 Test 코드 (인터페이스가 없는 경우, 구체 클래스)
  - proxyfactory - ProxyFactory 통한 프록시 (JDK 동적 프록시, CGLIB) 자동화 Test 코드
  - advisor - proxyFactory에 어드바이저 적용 Test 코드
  - postprocessor - 스프링 빈 후처리기 Test 코드
