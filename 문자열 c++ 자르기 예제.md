## 문자열 c++ 자르기 예제

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <cstring>

using namespace std;



//개발언어, 직군, 경력, 소울푸드, 점수,
//query가 조건, info가 지원서,

vector<int> solution(vector<string> info, vector<string> query) {
   vector<int> answer;
   string a = "";
   for (int i = 0; i < query.size(); i++)
   {
      vector<string>in;
      vector<string>qu;
      a = query[i];
      char *str2 = new char[100];//query

      strcpy(str2, a.c_str());
      char *token2 = strtok(str2, " ");

      while (token2 != nullptr)
      {
         qu.push_back(string(token2));
         token2 = strtok(nullptr, " ");
      }
      
      /*for (int i = 0; i < qu.size(); i++)
         cout << qu[i] << "\n";
      qu.clear();
      break;*/
      int count = 0;
      bool check = false;
      //정보순서-> 개발언어, 직군, 경력, 소울푸드, 점수
      for (int j = 0; j < info.size(); j++)
      {
         char *str = new char[100];//info
         
         strcpy(str, info[j].c_str());
         
         char *token = strtok(str, " ");//공백기준으로 나눔
         
         while (token != nullptr)
         {
            in.push_back(string(token));
            
         }
         for (int k = 0; k < in.size(); k++)
         {
            if (in[k] != qu[k] && k<=in.size()-2) {
               break;
            }
            else if((in[k]==qu[k] || qu[k]=="-") && k<=in.size()-2 )
            {
               check = true;
            }
            if (stoi(in[in.size()-1])>=stoi(qu[qu.size()-1]))
            {
               check = true;
            }
         }
         if (check == true)
            count++;
         in.clear();
         free(str);
         free(token);
      }
      answer.push_back(count);
      qu.clear();
      free(str2);
      free(token2);
      count = 0;
   }


   return answer;
}
```

