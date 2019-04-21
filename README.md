#include <algorithm>
#include <string.h>
#include <iostream> 
#include <stdio.h>
#include <vector>
#include <set>
#include <map>

#define boost ios_base::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define For(i, a, b, c) for (int i = a; i <= b; i += c)

typedef long long LL;
using namespace std;

namespace qu {
        void read(int &v) {
                int low = 0, l = 1;
                char ch;
                ch = getchar();
                for (; ch < '0' || ch > '9';) {
                        if ( ch == '-') l = -1;
                        ch = getchar();
                }
                for (; ch >='0' && ch <='9';) {
                        low = ( low << 1) + ( low << 3 ) + ( ch - 48);
                        ch = getchar();
                }
                v = l * low;
        }
        void print(int v) {
                if ( v < 0 ) putchar('-'), v *= -1;
                if ( v  > 9 ) print(v / 10);
                putchar(v % 10 + '0');
        }
}

class BigInt{
public:
    int num[100015];
    int size;
public:
    BigInt(){
        size = 0;
        memset(num,0,sizeof(num));
    }
    BigInt(int n){
        memset(num,0,sizeof(num));
        size = 0;
        while(n>0){
            num[size++] = n % 10;
            n /= 10;
        }
    }
    BigInt(string s){
        memset(num,0,sizeof(num));
        size = 0;
        int k = 0;
        while(s[k] == '0')
            k++;
        for(int i = s.length()-1; i >= k; i--){
            num[size++] = s[i] - '0';
        }
    }
 
    bool operator<(BigInt a){
        if(this->size != a.size){
            return this->size < a.size;
        }
        for (int i = 0; i < size; ++i){
            if(num[i] != a.num[i])
                return num[i]<a.num[i];
        }
        return false;
    }
 
    BigInt operator +(BigInt a){
        BigInt c;
        int k;
        for(k = 0; k<size && k<a.size; k++){
            c.num[k] = num[k] + a.num[k];
        }
        while(k < size){c.num[k] += num[k];k++;}
        while(k < a.size){c.num[k] += a.num[k];k++;}
        c.size = size>a.size?size:a.size;
        for (int i = 0; i < c.size; ++i){
            if(c.num[i]>=10){
                c.num[i+1] += c.num[i] / 10;
                c.num[i] %= 10;
            }
        }
        if(c.num[c.size] > 0)
            c.size++;
        return c;
    }
 
    BigInt operator -(BigInt a){
        BigInt x,y;
        BigInt t;
        t.size = size;
        for (int i = 0; i < size; ++i){
            t.num[i] = num[i];
        }
        if(t < a){
            x = a;
            y = t;
        }
        else{
            x = t;
            y = a;
        }
        BigInt r;
        r.size = x.size;
        int k;
        for (k = 0; k < y.size; ++k){
            r.num[k] = x.num[k]-y.num[k];
        }
        while(k < x.size){
            r.num[k] = x.num[k];
            k++;
        }
        for (int i = 0; i < r.size-1; ++i)
        {
            if(r.num[i] < 0){
                r.num[i+1] --;
                r.num[i] += 10;
            }
        }
        while(r.num[r.size-1] == 0)
            r.size--;
        if(t<a)
            r.num[r.size-1] = -r.num[r.size-1];
 
        return r;
    }
 
    BigInt operator *(BigInt a){
        BigInt r;
        r.size = size + a.size;
        for (int i = 0; i < size; ++i){
            for (int j = 0; j < a.size; ++j){
                r.num[i+j] += num[i] * a.num[j];
            }
        }
        for (int i = 0; i < r.size-1; ++i){
            r.num[i+1] += r.num[i] / 10;
            r.num[i] %= 10;
        }
        while(r.num[r.size-1] == 0)
            r.size--;
        return r;
    }
 
    // BigInt operator /(int a){
    //     ;
    // }
 
    void show(){
        int k = size-1;
        while(num[k] == 0 && k>=0)
            k--;
        if(k<0)
            k = 0;
        for (int i = k; i >=0 ; --i){
            printf("%d", num[i]);
        }
        printf("\n");
    }
};

LL pow(LL a, LL b, LL mod) {
        LL res = 1;
        while (b) {
                if (b & 1) res = (res * a) % mod;
                b >>= 1;
                a = (a * a) % mod;
        }
        return res;
}
int main() {
    boost;
    return 0;
}
