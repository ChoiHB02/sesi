# ParserAsset

---

<aside>
💡 **HEADER**

</aside>

---

# 개요

---

에셋 파일 안의 데이터를 빼는 방법과 데이터를 순서대로 엑셀에 넣는 것에 대한 문서

<aside>
⚠️ 작성시기 2023년 03월

</aside>

<aside>
⚠️ Visual Studio 2022, Excel 2013에서 진행되었습니다.

</aside>

---

* 사용 목적
  1. ASSET 확장자 파일에서 필요한 값들을 뽑아서 엑셀에 넣어서 정렬시키는 것.

* 구성 요소
    1.  데이터를 뽑을 에셋 파일이 담긴 폴더
    2.	데이터를 엑셀로 뽑아내서 저장할 폴더 


## 준비 작업

1. 먼저 프로젝트를 만들기 전에 Visual Studio Installer에 들어간다.
2. 워크로드 칸에 '.NET 데스크콥 개발'이라고 써져 있는 칸을 클릭하고 설치해주면, 준비가 끝난다.


## 코드 사용 방법

1. 먼저 Visual Studio에서 '새 프로젝트를 만들기'를 클릭해준다. 
2. 설치를 해줄 프로젝트는 '콘솔 앱(.NET Framework)'(C#) 이니 검색을 하거나 스크롤을 내려서 찾는다.
3. 이후에 새 창이 나오는데 이 글 밑에 있는 코드를 붙여넣으면 된다.
4. 이 코드를 하기 전 Visual Studio 2022에서는 프로젝트->참조 추가->COM->검색에서 'Excel' 타이핑 해주면 Microft Excel 15.0 Object Library가 나오는데 왼쪽 상자를 클릭하여 추가하고 확인을 눌러줘야 합니다.
5. 마지막으로 에셋파일이 들어있는 폴더의 경로를 찾고 경로의 길이를 재야한다.

 - 경로를 찾았다면 세 개의 변수를 바꿔줘야한다.
 ### 첫 번째 
 ```C#
string directoryPath = @"엑셀로 바꿀 폴더의 ";
```
 - 이 변수는 엑셀로 바꿀 폴더의 경로를 정해줘야한다.
 - 그렇기에 폴더로 가서 경로를 복사해주고 쌍따옴표 안에 붙여넣기를 한다.

 ### 두 번째 
```C#
 Directory.CreateDirectory(path[0] + "\\" + path[1] + "\\" + path[2] + "\\" + path[3] + "\\" +
  path[4] + "\\" + path[5]);
```
 - 이 변수는 디렉토리를 따로 하나 복사해서 엑셀로 바꾼 파일들을 넣는다. 
 - \마다 나눴기 때문에 길이에 따라 수정을 해줘야한다.
 - 예를 들어보자면 C:\Users\SESI\Downloads\homework\testFinal 에 파일이 담겨 있는 폴더들이 있으면 
 - C:이 path[0]이고 User가 path[1], SEST가 path[2]. 이런 식으로 길이에 따라 넣으면 되니 이건 path[5]까지 넣으면 될 것 같다.

 ### 세 번째 
```C#
 string savePath = path[0] + "\\" + path[1] + "\\" + path[2] + "\\" + path[3] + "\\" +
  path[4] + "\\" + path[5] + "\\" + fileName[0];
```
 - 엑셀 파일을 저장하는 경로 설정하는 변수이다.
 - 아까 폴더의 경로를 설정해왔으니 그걸 복사 붙여넣기를 하고 마지막에 + path[5] + "\\" + fileName[0] 를 넣으면 될 것 같다. 
 - 이렇게 하면 각 에셋 파일이 모두 엑셀 파일로 바뀌어진 광경을 볼 수 있다.


그럼 이제 두 개의 네임스페이스를 가져올 수 있는데 
```C#
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;
```
이 두 개는 C# 코드 내에서 Excel 통합 문서, 워크시트, 셀 및 기타 관련 개체에 액세스하고 조작할 수 있습니다.
먼저 엑셀을 만들기 위해선 이 두 개의 네임스페이스가 필요합니다. 

- 첫 번째 줄은 네임스페이스에 대한 별칭 "Excel"을 만듭니다. 
이렇게 하면 코드의 다른 네임스페이스 또는 클래스와의 이름 충돌을 방지할 수 있습니다.
- 두 번째 줄은 C# 코드에서 Excel 작업을 자동화하는 데 사용할 수 있는 모든 클래스, 인터페이스 및 열거형을 포함하는 전체 Excel 개체 모델을 가져옵니다.
---------------------------------------------------------------------------------------------------------------------------------------------

* 나머지 네임 스페이스
 - System.Text: 텍스트를 인코딩, 디코딩 및 조작하기 위한 형식과 클래스를 제공합니다.
 - System.Threading.Tasks: TAP(작업 기반 비동기 패턴)를 사용하여 비동기 코드를 작성하기 위한 형식과 클래스를 제공합니다.
 - System.Runtime.InteropServices: C# 코드에서 DLL 함수를 호출하는 것과 같이 비관리 코드와 상호 작용하기 위한 형식 및 클래스를 제공합니다.
 - System.Data.Common: 공용 ADO.NET 인터페이스를 구현하는 데이터 공급자와 함께 작업하기 위한 형식과 클래스를 제공합니다.
---------------------------------------------------------------------------------------------------------------------------------------------






## 에셋 파일 안의 데이터를 엑셀로 뽑아내는 전체 코드

```C#
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System.Runtime.InteropServices;
using Excel = Microsoft.Office.Interop.Excel;
using Microsoft.Office.Interop.Excel;
using System.Data;



namespace Excel_parseer
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.OutputEncoding = Encoding.GetEncoding("Shift-JIS");

            string directoryPath = @"엑셀로 바꿀 폴더의 ";

            // Get all file paths in the directory with the .asset extension
            //string[] excelFilePaths = Directory.GetFiles(directoryPath, "*.asset", SearchOption.AllDirectories);
            string[] excelFilePaths = Directory.GetFiles(directoryPath, "*.asset", SearchOption.AllDirectories)
             .Where(filePath => Path.GetFileName(filePath).Length <= 30)
             .ToArray();


            foreach (string excelFilePath in excelFilePaths)
            {
                Application excel = new Application();
                Workbook workbook = excel.Workbooks.Add();
                Worksheet worksheet = workbook.Sheets[1]; //storytimeline
                Worksheet worksheet2 = workbook.Sheets[1]; //title_color

                Console.WriteLine(excelFilePath);
                // asset 파일 경로
                //string assetFilePath = "C:\\Users\\SESI\\Downloads\\homework\\source\\Bundle\\Resources\\Story\\Data\\04\\1001\\storytimeline_041001001.asset";
                
                string[] path = excelFilePath.Split('\\'); // 파일 경로를 구분 
                string[] fileName = path[12].Split('.'); // 파일 네임에서 확장자를 뺌
                                                         // 텍스트 파일 경로
                                                         // string textFilePath = Path.ChangeExtension(assetFilePath, ".txt");
                                                         // asset 파일 내용을 텍스트 파일로 저장
                                                         //File.WriteAllText(textFilePath, File.ReadAllText(assetFilePath));

                Directory.CreateDirectory(path[0] + "\\" + path[1] + "\\" + path[2] + "\\" + path[3] + "\\" +
                    path[4] + "\\" + "testFinal\\" + path[6] + "\\" + path[7] + "\\" + path[8] + "\\" + path[9] + "\\"
                    + path[10] + "\\" + path[11]); //폴더 생성

                string[] lines = File.ReadAllLines(excelFilePath); //라인으로 텍스트의 글들을 싹 읽어 온거


                // 추출할 변수
                string variable_Text = " Text: \""; //storytimeline 시트에 text 칸에 넣는다.
                string variable_Name = "  Name:"; // storytimeline 시트에 name 칸에 넣는다.   
                string variable_Choice = "    NextBlock:"; // storytimeline 시트에 Choicelist 일 경우 name에 선택지라는 글을 넣고 text에 유니코드를 넣는다.
                string variable_Title = "Title: \""; //title_color 시트에서 text 칸에 넣는다.
                string NextBlock = "  NextBlock:";
                string DifferenceType = "  DifferenceType:";
                string DifferenceType2 = "    DifferenceType:";
                string DifferenceType3 = "  - Text: \""; //초이스 항목 중에 텍스트를 이용한 조건            //  DifferenceType: 1
                string Reload = "---";
                string Row1Array = null;
                string Row2Array = null;
                //DifferenceFlag: 2 둘의 옵션을 가지고 있는 오브젝트는   NextBlock:3 -> ChoiceList[] 1.NextBlock:4 2.NextBlock:4 
                //단 주인 오브젝트만 해당됨

                worksheet.Name = fileName[0];

                // 파일 네임에서 확장자를 뺀 변수를 시트 이름으로 지정
                worksheet = (Excel.Worksheet)workbook.Worksheets.get_Item(1);

                worksheet.Cells[1, 1] = "path";
                worksheet.Cells[1, 2] = "filename";
                worksheet.Cells[1, 3] = "name";
                worksheet.Cells[1, 4] = "name_kr";
                worksheet.Cells[1, 5] = "text";
                worksheet.Cells[1, 6] = "text_kr";
                worksheet2 = (Excel.Worksheet)workbook.Worksheets.Add(Type.Missing, worksheet, Type.Missing, Type.Missing);
                /// 시트2에 내용 집어넣기
                if (workbook.Worksheets.Count >= 2)
                {

                    worksheet2.Name = "title_color";

                    worksheet2.Cells[1, 1] = "path";
                    worksheet2.Cells[1, 2] = "filename";
                    worksheet2.Cells[1, 3] = "text";
                    worksheet2.Cells[1, 4] = "text_kr";
                }
                else
                {
                    Console.WriteLine("해당 워크북에 두 번째 워크시트가 존재하지 않습니다.");
                }

                int row = 2;
                int count = 0;

                foreach (string line in lines)
                {
                    if (line.Contains(NextBlock)) //nextblock 에서 뽑아낸 정수로 문장정렬
                    {
                        count++;

                    }
                }
                int[] nextBlocks = new int[count];
                string[] values3_Name = new string[count];
                string[] values3_Text = new string[count];

                bool ChoiceOne = false;
                bool Gates = false;
                bool sibaljum = false;
                bool sibaljum_Row = false;
                bool sibaljum2 = false;
                bool sibaljum3_1 = false;
                bool sibaljum3_2 = false;
                bool One_sibaljum = false;
                string[] values2_Name = null;
                string[] values2_Text = null;

                int Stepup = 0;
                int CountRow = 0;
                int different = 0;
                int variableblock = 0;
                int ChoiceNumber = 0;
                int row1 = 0; int row2 = 0;
                for (int i = 2; i <= count; i++) //i를 이용해서 순서대로 출력하게 만든다.
                {
                    values2_Name = null;
                    values2_Text = null;

                    foreach (string line in lines)  // nextBlock: i 를 찾는다.
                    {
                        if (line.Contains(variable_Name)) // Check if the line contains "Name: "
                        {

                            string[] values = line.Split(':');
                            values[1] = null;
                            values = line.Split(':');
                            //Name:
                            if (values[1] == " ") //"Name:" 이란 변수는 있는데 값이 없을 경우 
                            {
                                // values2_Name = line.Split(':');
                                string decoded = System.Text.RegularExpressions.Regex.Unescape(values[1]); //이스케이프 시퀀스를 디코딩할 수 있습니다. 
                                values2_Name = decoded.Split('\"');
                                //RowMinus1 =true;
                            }
                            if (!string.IsNullOrEmpty(values[1]))
                            {

                                string decoded = System.Text.RegularExpressions.Regex.Unescape(values[1]); //이스케이프 시퀀스를 디코딩할 수 있습니다. 
                                values2_Name = decoded.Split('\"');
                                //worksheet.Cells[row, 3] = values2_Name[1].Trim();
                                //RowMinus2 = true;
                            }

                        }
                        else if (line.Contains(variable_Choice)) //choice 쪽인데 Name을 출력해야 하는 경우 variable_Choice = "    NextBlock:"
                        {
                            string[] values = line.Split(':');
                            if (int.Parse(values[1]) == variableblock + 1)
                            {
                                sibaljum = true; //이걸 출력을 제한하는 용도로 씀
                                One_sibaljum = true;//이걸 출력을 제한하는 용도로 씀 무조건 처음만 +1을 하도록 함
                                                    //Console.WriteLine(variableblock);
                                sibaljum_Row = true;

                            }


                            //worksheet.Cells[row, 3] = "선택지"; //ChoiceList를 Name 쪽에 "선택지"로 저장
                            if (int.Parse(values[1]) == i)
                            {
                                ChoiceOne = true;
                            }

                        }
                        if (line.Contains(variable_Text)) // Check if the line contains "Text: "
                        {

                            string[] values = line.Split(':');
                            string japaneseString = values[1].Trim(); // Remove leading/trailing space
                            string decoded = System.Text.RegularExpressions.Regex.Unescape(japaneseString); //이스케이프 시퀀스를 디코딩할 수 있습니다. 
                            values2_Text = decoded.Split('\"');


                            //path[6~11] 
                            worksheet.Cells[row, 1] = path[6].Trim() + "\\" + path[7].Trim() + "\\" + path[8].Trim() + "\\" + path[9].Trim() + "\\" +
                                path[10].Trim() + "\\" + path[11].Trim(); //Path 출력

                            //path[12] 
                            worksheet.Cells[row, 2] = fileName[0].Trim(); //Filename 출력


                            Gates = true;
                        }
                        if (line.Contains(DifferenceType))
                        {
                            string[] values = line.Split(':');
                            if (int.Parse(values[1]) == 1) //DifferenceType이 1이라면 변수 1 정의   DifferenceType:
                            {
                                different = 1;
                            }
                            else // DifferenceType이 1이 아니라면 거부
                            {
                                different = 0;
                            }
                        }
                        if (line.Contains(DifferenceType2)) //거름망2 "    DifferenceType:";
                        {
                            string[] values = line.Split(':');

                            different = 0;

                        }
                        if (line.Contains(DifferenceType3)) // 초이스 항목 중에 텍스트를 이용한 조건 "  - Text: \""
                        {
                            ChoiceNumber++;
                        }
                        if (line.Contains(NextBlock))//NextBlock: "  NextBlock:"  
                        { //NextBlock을 숫자순으로 차례대로 검사하여 엑셀에 저장

                            string[] values = line.Split(':');
                            if (Stepup - 1 == int.Parse(values[1]))
                            {
                                CountRow = 8;
                            }
                            if (Gates == true) //Text 변수에서 문장을 가져왔을 때
                            {
                                if (different == 1) // 유일한 문제 여기서 different는 처음에만 작용하고 후에 초이스에 관한 조건을 부정한다.
                                {
                                    if (sibaljum == true) //여기서 나온 정수들은 첫 번째로 나온 것을 +1을 시킨다. 그리고 
                                    {
                                        //아마 여기서 i++을 시키면 될듯?
                                        if (One_sibaljum == true) //첫 번째만 적용
                                        {
                                            i++;
                                            sibaljum2 = true;
                                        }
                                        ChoiceOne = true;
                                        One_sibaljum = false;
                                        Console.WriteLine(i); //4, 44 가 나온다.
                                        Console.WriteLine(int.Parse(values[1])); //4, 44가 나온다.
                                        Stepup = int.Parse(values[1]);
                                    }
                                }
                            }
                            if (int.Parse(values[1]) == i)//i를 이용해서 순서대로 출력하게 만든다.
                            {

                                if (Gates == true) //Text 변수에서 문장을 가져왔을 때
                                {
                                    //출력했던 문장을 빼내는 문단.
                                    if (ChoiceOne == true)
                                    {
                                        worksheet.Cells[row, 3] = "선택지";

                                    }
                                    else
                                    {
                                        if (values2_Name.Length >= 2)
                                        {
                                            variableblock = int.Parse(values[1]);
                                            worksheet.Cells[row, 3] = values2_Name[1];

                                        }
                                        else
                                        {
                                            worksheet.Cells[row, 3] = "";
                                            // 배열의 길이가 충분하지 않은 경우 예외 처리
                                        }
                                    }
                                    worksheet.Cells[row, 5] = values2_Text[1];
                                    row++;
                                    Gates = false;
                                }

                            }

                        }
                        if (line.Contains(Reload)) //구분자가 끝나는 곳이므로 초기화를 하는 곳이다. "---";
                        {
                            if (sibaljum == true && ChoiceNumber >= 1 && sibaljum2 == true) // i을 -1한다.
                            {

                                if (ChoiceNumber == 1)
                                {
                                    i--;
                                    Console.WriteLine(i + "R1");
                                    //row -= 1;
                                }
                                if (ChoiceNumber == 2)
                                {
                                    i--;
                                    Console.WriteLine(i + "R2");
                                    //row -= 2;
                                }

                            }
                            if (ChoiceOne == true && ChoiceNumber >= 1 && (CountRow == 8) && sibaljum_Row == true) // Row를 뺀다
                            {

                                if (ChoiceNumber == 1)
                                {

                                    sibaljum3_1 = true;
                                    CountRow = 0;
                                    sibaljum_Row = false;
                                    row -= 1;
                                    Row1Array += row + ".";
                                    row1 = row;
                                }
                                if (ChoiceNumber == 2)
                                {

                                    sibaljum3_2 = true;
                                    CountRow = 0;
                                    sibaljum_Row = false;
                                    row -= 2;
                                    Row2Array += row + ".";
                                    row2 = row;
                                }
                            }
                            different = 0; //deferent 초기화

                            variableblock = 0;

                            ChoiceNumber = 0;
                            Stepup = 0;
                            ChoiceOne = false;
                            sibaljum = false;
                            sibaljum2 = false;

                        }

                        /////
                        if (line.Contains(variable_Title)) //Title 시트 값 저장
                        {
                            if (line.Contains("\""))
                            {
                                string[] values = line.Split(':');

                                string japaneseString = values[1].Trim(); // Remove leading/trailing whitespac
                                string decoded = System.Text.RegularExpressions.Regex.Unescape(japaneseString);
                                values2_Text = decoded.Split('\"');
                                worksheet2.Cells[2, 3] = values2_Text[1].Trim();
                            }
                            else
                            {
                                string[] values = line.Split(':');
                                string japaneseString = values[1].Trim();
                                worksheet2.Cells[2, 3] = japaneseString.Trim();
                            }


                            //path[6~11] 
                            worksheet2.Cells[2, 1] = path[6].Trim() + "\\" + path[7].Trim() + "\\" + path[8].Trim() + "\\" + path[9].Trim() + "\\" +
                                path[10].Trim() + "\\" + path[11].Trim(); //Path 출력

                            //path[12] 

                            worksheet2.Cells[2, 2] = fileName[0].Trim(); //Filename 출력

                            worksheet2.Cells[2, 5] = "title";
                        }

                    }

                }



                foreach (string line in lines)  // NextBlock: -1를 찾아서 출력.
                {

                    if (line.Contains(variable_Name)) // Check if the line contains "Name: "
                    {
                        string[] values = line.Split(':');
                        //Name:
                        if (values[1] == " ") //"Name:" 이란 변수는 있는데 값이 없을 경우 
                        {
                            values2_Name[1] = " ";
                        }
                        else
                        {
                            string decoded = System.Text.RegularExpressions.Regex.Unescape(values[1]); //이스케이프 시퀀스를 디코딩할 수 있습니다. 
                            values2_Name = decoded.Split('\"');
                        }
                    }
                    if (line.Contains(variable_Text)) // Check if the line contains "Text: "
                    {

                        string[] values = line.Split(':');
                        string japaneseString = values[1].Trim(); // Remove leading/trailing space
                        string decoded = System.Text.RegularExpressions.Regex.Unescape(japaneseString); //이스케이프 시퀀스를 디코딩할 수 있습니다. 
                        values2_Text = decoded.Split('\"');

                    }
                    int i = -1;
                    if (line.Contains(NextBlock))//NextBlock: "  NextBlock:"  
                    { //NextBlock을 숫자순으로 차례대로 검사하여 엑셀에 저장
                        string[] values = line.Split(':');
                        if (int.Parse(values[1]) == i)
                        {


                            worksheet.Cells[row, 3] = values2_Name[1].Trim();
                            worksheet.Cells[row, 5] = values2_Text[1];


                        }

                    }


                }
                string[] arr = null;
                if (sibaljum3_1 == true)
                {
                     arr = Row1Array.Split('.');
                }
      
                Console.WriteLine(Row1Array);
                string cell;
                if (sibaljum3_1 == true)
                {
                    for (int y = 0; y < arr.Length - 2; y++)
                    {
                        cell = worksheet.Cells[int.Parse(arr[y]), 3].Value;
                        worksheet.Cells[int.Parse(arr[y]), 3].Value = worksheet.Cells[int.Parse(arr[y]) + 1, 3].Value;
                        worksheet.Cells[int.Parse(arr[y]) + 1, 3].Value = cell;

                        cell = worksheet.Cells[int.Parse(arr[y]), 5].Value;
                        worksheet.Cells[int.Parse(arr[y]), 5].Value = worksheet.Cells[int.Parse(arr[y]) + 1, 5].Value;
                        worksheet.Cells[int.Parse(arr[y]) + 1, 5].Value = cell;
                        // sibaljum3_1 = false;
                        Console.WriteLine(arr[y]);

                    }

                }
                string[] arr1 = null;
                if (sibaljum3_2 == true)
                {
                    arr1 = Row2Array.Split('.');
                }
               

                Console.WriteLine(Row2Array);
                if (sibaljum3_2 == true)
                {
                    for (int y = 0; y < arr1.Length - 2; y++)
                    {
                        // Swap values in column 3
                        Console.WriteLine(int.Parse(arr1[y]));
                        cell = worksheet.Cells[int.Parse(arr1[y]), 3].Value;
                        worksheet.Cells[int.Parse(arr1[y]), 3].Value = worksheet.Cells[int.Parse(arr1[y]) + 1, 3].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 1, 3].Value = cell;
                        cell = worksheet.Cells[int.Parse(arr1[y] + 1), 3].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 1, 3].Value = worksheet.Cells[int.Parse(arr1[y]) + 2, 3].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 2, 3].Value = cell;

                        // Swap values in column 5
                        cell = worksheet.Cells[int.Parse(arr1[y]), 5].Value;
                        worksheet.Cells[int.Parse(arr1[y]), 5].Value = worksheet.Cells[int.Parse(arr1[y]) + 1, 5].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 1, 5].Value = cell;
                        cell = worksheet.Cells[int.Parse(arr1[y] + 1), 5].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 1, 5].Value = worksheet.Cells[int.Parse(arr1[y]) + 2, 5].Value;
                        worksheet.Cells[int.Parse(arr1[y]) + 2, 5].Value = cell;
                        sibaljum3_1 = false;

                    }

                }
                //엑셀를 저장하는 경로 설정
                string savePath = path[0] + "\\" + path[1] + "\\" + path[2] + "\\" + path[3] + "\\" +
                    path[4] + "\\" + "testFinal\\" + path[6] + "\\" + path[7] + "\\" + path[8] + "\\" + path[9] + "\\"
                    + path[10] + "\\" + path[11] + "\\" + fileName[0];

                workbook.SaveAs(savePath, AccessMode: Excel.XlSaveAsAccessMode.xlExclusive,
    ConflictResolution: Excel.XlSaveConflictResolution.xlLocalSessionChanges);
                workbook.Close();
                excel.Quit();

                //clean up
                ReleaseExcelObject(worksheet);
                ReleaseExcelObject(workbook);
                ReleaseExcelObject(excel);
            }
        }
        private static void ReleaseExcelObject(object obj) // 엑셀 앱 정리
        {
            try
            {
                if (obj != null)
                {
                    Marshal.ReleaseComObject(obj);
                    obj = null;
                }
            }
            catch (Exception ex)
            {
                obj = null;
                throw ex;
            }
            finally
            {
                GC.Collect();
            }
            Console.WriteLine("Excel file created , you can find the file");
        }
    }

}


```


