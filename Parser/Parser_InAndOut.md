# Parser 인앤아웃

---

<aside>
💡 **HEADER**

</aside>

---

# 개요

---

엑셀 안의 데이터를 빼는 방법과 텍스트를 엑셀에 넣는 것에 대한 문서

<aside>
⚠️ 작성시기 2023년 03월

</aside>

<aside>
⚠️ Visual Studio 2022, Excel 2013에서 진행되었습니다.

</aside>

---

## 이 코드를 하기 전 Visual Studio 2022에서는 프로젝트->참조 추가->COM->검색으로 Excel 타이핑을 하면 Microft Excel 15.0 Object Library가 나오는데 왼쪽 상자를 클릭하여 추가하고 확인을 눌러줘야한다.

## 엑셀 안의 데이터를 텍스트화 시키는 코드

엑셀의 데이터들을 텍스트로 변환시키는 코드
분리된 셀의 정의를 ';'로 지정하여 가로줄의 텍스트를 뽑아낸다.  
* 먼저 테스트로 뽑아낼 파일의 위치를 지정해주세요.
* xlApp.Workbooks.Open 함수 옆에 위치를 지정하는 곳에 넣으면 됩니다.

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System.Runtime.InteropServices;
using System.Data.OleDb;
using System.IO;
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;


namespace Excel_read
{
    internal class Program
    {
        static void Main(string[] args)
        {
            
            Console.OutputEncoding = Encoding.Unicode; //일본 한자를 출력하게 만들어주는 코드
            string str;
            int rCnt;
            int cCnt;
            int rw = 0; //행 개수
            int cl = 0; //열 개수
            // 엑셀 범위의 대한 필요한 변수들을 선언
            
            Excel.Range range; //엑셀 범위 선언

            Excel.Application xlApp =new Microsoft.Office.Interop.Excel.Application(); //Excel.Application 객체는 Excel 프로그램을 제어할 수 있는
                                                                                       //기능을 제공하는 COM(Component Object Model) 객체


            //Excel Workbook은 Excel 파일 자체를 나타내는 객체입니다.
            //즉, 엑셀 파일 내에 있는 각각의 시트들과 데이터들을 포함하는 최상위 객체입니다.
            Excel.Workbook xlWorkBook = xlApp.Workbooks.Open(@"C:\Users\SESI\Downloads\language.howtoplay.xlsx", 0, true, 5, "", "", 
                true, Microsoft.Office.Interop.Excel.XlPlatform.xlWindows, "\t", false, false, 0, true, false, 0);
            //1.파일 경로 및 이름: @"d:\csharp-Excel.xls", 2.파일의 링크가 업데이트되는 방식을 지정합니다. 인수가 2인 경우 파일에 첨부된 그래프에서 차트를 생성합니다. 인수가 0이면 차트가 만들어지지 않습니다.

            //3.읽기 전용: true (통합 문서를 읽기 전용 모드로 열 경우), 4. 엑셀 문서 내의 구분 기호 지정: 5 (생략하면 현재 구분 기호 사용됨)

            //5.암호: "" (파일이 암호화되어 있지 않으므로 빈 문자열을 입력), 6.통합 문서에 암호: "" (쓰기 예약 통합 문서에 쓰는 데 필요한 암호가 들어 있는 문자열),

            //7.IgnoreReadOnlyRecommended: ture (Microsoft Excel에서 읽기 전용 권장 메시지를 표시하지 않도록 하려면 True), 

            //8.Origin: Microsoft.Office.Interop.Excel.XlPlatform.xlWindows (Windows용 Excel 파일,파일이 텍스트 파일인 경우 이 인수는 파일이 시작된 위치를 나타냅니다),

            //9.필드 구분 기호(Delimiter): "\t" (탭으로 구분되는 필드가 있는 경우)  Format 인수가 6인 경우 이 인수는 구분 기호로 사용할 문자를 지정하는 문자열입니다.
            //예를 들어 탭에는 Chr(9)를 사용하고,
            //쉼표에는 ","를 사용하고, 세미콜론에는 ";" 를 사용하거나, 사용자 지정 문자를 사용합니다. 문자열의 첫 번째 문자만 사용됩니다.

            //10.워크시트를 읽을 수 있는지 여부: false (워크시트가 비밀번호로 보호되어 있는 경우) 11.편집가능한지: false (파일을 편집용으로 열지 않음),

            //12.파일을 열 때 시도할 첫 번째 파일 변환기의 인덱스(Converter): 0 (변환기 인덱스는 FileConverters 속성에서 반환하는 변환기의 행 번호로 구성됩니다.),

            //13.통합 문서를 최근에 사용한 파일 목록에 추가: true (추가하려면 True입니다. 기본값은 False입니다.)

            //14.Local: 1 True는 Microsoft Excel의 언어(제어판 설정 포함)에 대해 파일을 저장합니다. False(기본값)는 VBA(Visual Basic for Applications)
            //언어(통합 문서.Open이 실행되는 VBA 프로젝트가 이전의 국제화된 XL5/95 VBA 프로젝트가 아닌 경우 일반적으로 미국 영어)에 대해 파일을 저장합니다.

            //15.CorruptLoad: 0 (Workbook is opened normally.)(값을 지정하지 않은 경우의 기본 동작은 xlNormalLoad이며 OM을 통해 시작될 때 복구를 시도하지 않습니다.)

            //근데 수정할 거 없으면 그냥 파일 경로만 불러서 호출 가능함 (파일 경로만 필수)


            Excel.Worksheet xlWorkSheet = (Excel.Worksheet)xlWorkBook.Worksheets.get_Item(1); //열린 Workbook 객체에서 첫 번째 Worksheet 객체를 가져옵니다.

            range = xlWorkSheet.UsedRange;
            rw = range.Rows.Count; // 행 개수 대한 범위 선언 
            cl = range.Columns.Count; // 열 개수 대한 범위 선언

            for (rCnt = 1; rCnt <= rw; rCnt++)
            {
                for (cCnt = 1; cCnt <= cl; cCnt++)
                {
                    str = (string)(range.Cells[rCnt, cCnt] as Excel.Range).Value2; //현재 셀 값을 가져옵니다.
                    Console.Write(str); // 데이터를 출력
                    if (((string)(range.Cells[rCnt, cCnt+1] as Excel.Range).Value2 == null) && ((string)(range.Cells[rCnt, cCnt+2] as Excel.Range).Value2 == null)) // 한, 두 칸 앞에 자료가 없을 경우 ;를 붙이지 않고 넘어감
                    {
                        continue;
                    }
                    Console.Write(";"); // 셸에 들어있는 데이터의 출력이 끝나면 세미콜론(;) 출력 
                }
                Console.WriteLine(); // 줄바꿈
            }

            xlWorkBook.Close(true, null, null); 
            xlApp.Quit();
            //Workbook 객체와 Excel 어플리케이션 객체를 종료합니다.

            Marshal.ReleaseComObject(xlWorkSheet);
            Marshal.ReleaseComObject(xlWorkBook);
            Marshal.ReleaseComObject(xlApp);

        }
    }
}

```




## 텍스트안에 있는 데이터를 엑셀로 옮기는 코드

텍스트의 데이터들을 엑셀 로 변환시키는 코드
텍스트 속의 셀의 단위를 ';'지정하여 나누어줍니다.
* 먼저 테스트로 뽑아낼 파일의 위치를 지정해주세요.
* File.ReadAllLines 함수 옆에 위치를 지정하는 곳에 넣으면 됩니다.


```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System.Runtime.InteropServices;
using System.Data.OleDb;
using System.IO;
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;
using System.Drawing;


namespace Excel_makeByText
{
    internal class Program
    {
        static void Main(string[] args)
        {
            
            Application excel = new Application();// 어플리케이션 선언 
            Workbook workbook = excel.Workbooks.Add(); // 워크 북 더하기
            Worksheet worksheet = workbook.Sheets[1]; // 데이터를 넣을 워크 시트 선언 
            string[] lines = File.ReadAllLines(@"C:\\Users\\SESI\\Downloads\\language.howtoplay.txt"); // 텍스트 파일을 읽을 경로 설정 

            int row = 1;
            foreach (string line in lines)
            {
                string[] values = line.Split(';'); //텍스트 안의 글자들 속에 ';'마다 셀로 나누어줍니다.
                int column = 1;
                foreach (string value in values)
                {
                    worksheet.Cells[row, column] = value; // 순서대로 글자를 셀에 입력해줍니다.
                    worksheet.Columns[column].AutoFit(); // 글자의 길이에 따라 셀이 늘어나는 코드
                    worksheet.Cells[row, column].WrapText = true; //셸이 줄바꿈이 되는 코드
                    column++;
                }
                row++;
            }

            string savePath = @"C:\Users\SESI\Downloads\Excel_practice\output.xlsx"; //엑셀파일을 저장할 경로를 설정
            workbook.SaveAs(savePath); // 엑셀 파일저장
            workbook.Close(); // 워크 북 종료
            excel.Quit(); // 엑셀 나가기
        }
    }
}
```
