#Spring

## @RequestBody, @ResponseBody
1) RequestBody 동작
  - @RequestBody를 처리할 수 있는, resolver를 가져온다(RequestResponseBodyMethodProcessor)
  - 해당 Resolver에 등록되어 있는 Converter 중 MappingJackson2HttpMessageConverter 에서 body 정보를 생성한다
    - 생성 시 ObjectMapper 활용
  - 리플렉션을 통해 가져온 body값을 controller의 파라미터에 invoke 해주면서 데이터가 dto에 binding 된다.
