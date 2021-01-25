# N-Queens
public class Solution {
    private ArrayList<List<String>> helper(char[][] cheeseboard, int n , ArrayList<List<String>> temp) {
	    //跑完整個棋盤格後，開始塞入結果
        if(n == cheeseboard[0].length)
        {  
            ArrayList<String> temp1 = new ArrayList<>();
            //個數滿就加入ArrayList內
            for(char [] temp_board : cheeseboard)
                temp1.add(new String(temp_board));
            //回傳最後結果
            temp.add(temp1);
        }
        for(int i=0 ; i<cheeseboard.length; i++){
            if(IfCanPut(cheeseboard,i,n)){
                 //放皇后
                 cheeseboard[i][n]='Q';
				 //跑遞迴
                 helper(cheeseboard,n+1,temp);
                 //一旦在 cheeseboard[i][n]這裡放皇后無法得到解答，就移除該皇后
                 cheeseboard[i][n]='.';
            }
        }
		return temp;
    }                                            //行     //列
    private boolean IfCanPut(char[][] cheeseboard,int row,int col) {
        //確認同行是否已經有皇后
        for (int i = 0; i < col; i++)
            if (cheeseboard[row][i] == 'Q')
                return false;
        //確認左上角是否有皇后
        for (int i=row, j=col; i>=0 && j>=0; i--, j--)
            if (cheeseboard[i][j] == 'Q')
                return false;
        //確認左下角是否有皇后
        for (int i=row, j=col; j>=0 && i<cheeseboard.length; i++, j--)
            if (cheeseboard[i][j] == 'Q')
                return false;
        return true;
    }
    public List<List<String>> solveNQueens(int n) {
        //模擬N*N棋盤
        char[][] cheeseboard = new char[n][n];
        //初始化陣列
        for (int i = 0; i < n; i++) 
            Arrays.fill(cheeseboard[i],'.');
            //回傳最後答案的ArrayList
        return helper(cheeseboard,0, new ArrayList<>());
    }
}
