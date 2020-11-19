## C++ 문자열 공백단위로 자르는 코드

```
#include <map>
#include <set>
#include <list>
#include <cmath>
#include <ctime>
#include <deque>
#include <queue>
#include <stack>
#include <string>
#include <bitset>
#include <cstdio>
#include <limits>
#include <vector>
#include <climits>
#include <cstring>
#include <cstdlib>
#include <fstream>
#include <numeric>
#include <sstream>
#include <iostream>
#include <algorithm>
#include <unordered_map>

using namespace std;
int numOfAttirute;
float threshold;
int n;//number of rows
vector<string>age;
vector<string>sex;
vector<string>education;
vector<string>country;
vector<string>race, marital, workclass, occupation, hours;
vector<string>income, capital_gain, capital_loss;
vector<string>info;
void checkThreshold(float s_threshold)
{
   
}

void sliceString(vector<string>info) {

   string t = "";
   for (int i = 0; i < info.size(); i++)
   {
      t = info[i];

      char *str = new char[1000];

      strcpy(str, t.c_str());
      char *token = strtok(str, ",");//,단위로 분리 

      while (token != nullptr)
      {
         if (token[0] == 'a')
         {
            age.push_back(string(token));
            token = strtok(nullptr, " ");
         }
      }

      free(str);
      free(token);
   }
   return;
}


int main() {
   /* Enter your code here. Read input from STDIN. Print output to STDOUT */

   cin >> numOfAttirute >> threshold >> n;
   string temp;
   for (int i = 0; i < n; i++)
   {
      getline(cin, temp);
      info.push_back(temp);
   }

   sliceString(info);
   checkThreshold(threshold);



   return 0;
}
```

___

설명: 문자열을 char배열에 저장하여 위의 코드는 ',' 단위로 토큰을 잘라서 문자열이 null을 만날때까지 토큰단위로 벡터에 구분하여 저장하는 코드입니다.