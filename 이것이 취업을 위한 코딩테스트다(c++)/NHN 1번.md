## NHN 1번

```
#include <vector>
#include <iostream>
#include <vector>

using namespace std;

//핵심 소스코드의 설명을 주석으로 작성하면 평가에 큰 도움이 됩니다.
class Solution{
public:
    int solution(vector<int> goods){
       int sum = 0;
   int all = 0,answer=0;
   bool check = false;
   int cnt = 0;

   for (int i = 0; i < goods.size(); i++)
   {
      if (goods[i] < 50)//50미만의 가격일 경우 sum의 변수에 합하여 50이상이 될때를 구합니다.
      {   
         sum += goods[i];
         if (sum >= 50) {//50미만의 물품의 합이 50이상이되면 할인 개수를 증가하고 sum을 초기화합니다.
            cnt++;
            sum = 0;
         }
         true;
      }
      else
      {
         cnt++;
      }
      all += goods[i];//총합
   }
    
   if (check == true) {
      answer =all- 30;
   }
   else {
      answer =all-cnt * 10;
   }


   return answer;
    }
};
```

