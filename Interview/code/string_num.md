# 大数的四则运算

这题目不是别人问到我的，而是最近在招人的时候喜欢问别人的一道题目，不过没想到的是五年工作经验以上的老同志好多都没答上来，或许是问题本身就有问题，但是题目却都是大三的课后习题....

## 加法/减法

正整数加法和减法思路类似一个是借位，一个是进位。依赖原始的竖式计算可得（如果是整数运算得有个规律:同号相加、异号相减，所以加法/减法要实现完全就得全部都做）：

```$java

    private static String sum(String a,String b){
        int sub = Math.abs(a.length() - b.length());
        StringBuilder subStr = new StringBuilder();
        for(int i=0;i<sub;i++){
            subStr.append("0");
        }
        if (a.length() > b.length()){
            b = subStr.toString() + b;
        }else {
            a = subStr.toString() + a;
        }
        char[] ca = a.toCharArray();
        char[] cb = b.toCharArray();


        int[] ia = IntStream.range(0, ca.length).map(i -> ca[i] - 48).toArray();
        int[] ib = IntStream.range(0, cb.length).map(i -> cb[i] - 48).toArray();

        int past = 0;
        int[] res = new int[ia.length];
        for (int i = ia.length-1; i>=0;i--){
            int t = ia[i]+ ib[i] + past;
            if (t >= 10) {
                res[i] = t % 10;
                past = 1;
            } else {
                res[i] = t;
                past = 0;
            }
        }

        StringBuilder rk = new StringBuilder();
        if (past > 0){
            rk.append(past);
        }
        for (int i :res){
            rk.append(i);
        }
        return rk.toString();
    }

```

同样的，减法在补位数的时候计算逻辑一样，只需要把进位改借位：
```$java
private static String sub(String a,String b){

        ···

        int past = 0;
        int[] res = new int[ia.length];
        if (!flag){
            int[] ic = ia;
            ia = ib;
            ib = ic;
        }
        for (int i = ia.length-1; i>=0;i--){
            int t = ia[i] - ib[i] + past;
            if (t < 0) {
                res[i] = 10 + t;
                past = -1;
            } else {
                res[i] = t;
                past = 0;
            }
        }

        StringBuilder rk = new StringBuilder();
        if (!flag){
            rk.append("-");
        }
        for (int i :res){
            rk.append(i);
        }
        return rk.toString();
    }

```
## 乘法

如果不使用印度乘法或者一些乘法分解的离谱算法，其实直接使用竖式计算的方式依然可以得出（若考虑负数单独计算--=+ +-=-）：