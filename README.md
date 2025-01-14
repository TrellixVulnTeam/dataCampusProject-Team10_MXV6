&#x1F4D9; A-Catcher
=========

**한국데이터산업협회 회장상 수상작**

**복잡한 한국어 텍스트를 읽기 쉬운 형태로 변환해주는 자연어처리 서비스** :loudspeaker:
---------------------------------------------------


*"Grab both Attention and Become an Ace with our A Catcher!"*  
     
*Attention*을 캐치해서 *Ace*가 되도록 도와주는 자연어처리 서비스
      
   **Highlight & Underline & POPup Text**
   
      - 어려운 텍스트의 중심문장과 단어, 그리고 연결고리를 파악할 수 있도록 다양한 도형과 색상으로 텍스트를 강조
      
   **Text to PPTX**
   
      - 발표 대본의 제목과 소제목을 자동으로 추출하여 텍스트를 파워포인트에 삽입
      - 텍스트 주제와 어울리는 피피티 템플릿 및 이미지 추천


### Examples

![Alt text](https://github.com/yoonkim313/dataCampusProject-Team10/blob/master/ServiceExample.png)
![Alt text](https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/example2.png)
--------------------------------------------------------------------------------------------------

### Structure

![Alt text](https://github.com/yoonkim313/dataCampusProject-Team10/blob/master/how.png)
---------------------------------------------------------------------------------------------------


   ###### ➊ OCR (Optical Character Recognition)
            pdf, jpeg, jpg, txt 등의 다양한 파일 입력 형식을 지원합니다. OCR을 통해 이미지에서 글자를 찾아내고 이 텍스트 파일을 기반으로 서비스를 제공합니다.
      
   ###### ➋ NLP (Relation Extraction & Extractive Summarization & Keyword Extraction)
            서비스의 핵심분야로써 본래의 줄글에서 단락별 중심문장, 중요한 단어들이 포함된 구절들, 그리고 한 문장안에서 단어들의 관계성을 정리하여 읽기 쉬운 형식으로 가공된 텍스트를 지원합니다.
            + Text2PPTX : 파워포인트의 XML 코드 형식을 분석하여 제목과 목차 그리고 관계형 도형으로 텍스트가 매핑되도록 모듈을 구축하였습니다.
      
   ###### ➌ Web Interface with python-based FLASK
            플래스크 기반의 웹 서버를 구축하여 사용자가 원하는 형식의 파일을 업로드하면 Graphical User Interface를 통해 서비스를 사용할 수 있도록 만들었습니다.

### Main page           
![Alt text](https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/main.png)
     
