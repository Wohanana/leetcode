# 题目描述：
将一个给定字符串 s 根据给定的行数 numRows ，以从上往下、从左到右进行 Z 字形排列。
比如输入字符串为 "PAYPALISHIRING" 行数为 3 时，排列如下：

    P   A   H   N
    A P L S I I G
    Y   I   R
# 解析：
## 按行排序
定义一个字符串列表，长度为min{numRows,s.length()}
只有当当前行号为0或者min{numRows,s.length()}-1时，行排序的方向才会变
代码如下：

    class Solution {
        public String convert(String s, int numRows) {
            if(numRows==1)  return s;
            List<StringBuilder> rows=new ArrayList<>();
            for(int i=0;i<Math.min(s.length(),numRows);i++){
                rows.add(new StringBuilder());
            }
            boolean goingDown=false;
            int currow=0;
            for(char c:s.toCharArray()){
                rows.get(currow).append(c);
                //当前行号为0或者min{numRows,s.length()}-1时，行排序的方向才会变
                if(currow==0||currow==Math.min(s.length(),numRows)-1)   goingDown=!goingDown;
                currow+=(goingDown?1:-1);
            }
            StringBuilder ans=new StringBuilder();
            for(StringBuilder row:rows){
                ans.append(row);
            }
        return ans.toString();
        }
    }
