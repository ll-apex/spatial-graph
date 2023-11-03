# LiveLabs의 변수

## 소개

다른 파일에서 변수를 지정하고 마크다운에서 참조할 수 있습니다.

## 태스크 1:

상단 섹션의 manifest.json에 다음을 추가합니다.

       "variables": ["../../variables/variables.json",
                     "../../variables/variables-in-another-file.json"],
    

## 태스크 2

.json 파일에 다음과 같이 변수를 지정합니다.

_예: variables.json_

    {
        "var1": "Variable 1 value",
        "var2": "Variable 2 value",
        "random_name": "LiveLabs rocks!",
        "number_of_ocpu_paid": "24"
        "number_of_ocpu_always_free": "2"
     }
    

변수를 지정하는 여러 파일을 추가할 수도 있습니다(작업 1의 예제 참조).

_예: variables\_in\_another\_file.json_

    {
        "var11": "Variable 1 value but yet different",
        "var22": "Variable 2 value is different",
        "random_name2": "LiveLabs rocks & rules!",
        "name_of_database": "My-Database-Name-is-the-best",
        "magic": "What is 2*2?"
     }
    

## 태스크 3

이제 다음 구문을 사용하여 해당 변수를 참조할 수 있습니다(**구문은 마크다운에서만 볼 수 있습니다**).

[](var:var1)

또는

[](var:magic)

### 예제

(구문을 보려면 마크다운을 선택합니다. 굵은 텍스트는 변수 값입니다.)

*   수학 아세요? **[](var:magic)**입니다.
    
*   유료 테넌시에서 이 서비스를 실행하려면 몇 개의 OCPU가 필요합니까? **[](var:number_of_ocpu_paid)**이 필요합니다.
    
*   하지만 '항상 무료'를 사용한다면 어떨까요? 그런 다음 **[](var:number_of_ocpu_always_free)**이 필요합니다.
    
*   데이터베이스에 가장 적합한 이름은 무엇입니까? **[](var:name_of_database)**입니다.
    
*   여기에서 추가 정보를 찾을 수 있습니다.**[](var:doc_link)**