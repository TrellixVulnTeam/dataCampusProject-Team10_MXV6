# Flask

---
## app.py
```python
app = Flask(__name__)
run_with_ngrok(app)

basedir = '/content/drive/Shared drives/BigDATA TEAM 10/dataCampusProject-Team10/flask' 
upload_dir = os.path.join(basedir, 'uploads')  # basedir 의 uploads 에 파일 저장
############################################################################################################

admin = Admin(name='Uploaded Files')
admin.init_app(app) 
dropzone = Dropzone(app)
admin.add_view(FileAdmin(upload_dir, name='FILES')) 
app.config['DROPZONE_ALLOWED_FILE_CUSTOM'] = True
app.config['DROPZONE_ALLOWED_FILE_TYPE'] = 'image/*, .pdf, .txt'
############################################################################################################

@app.route("/", methods=['GET', 'POST'])
def upload():
    if request.method == 'POST':
        f = request.files.get('file')
        f.save(os.path.join(upload_dir, f.filename))
        images = convert_from_path(os.path.join(upload_dir, f.filename))
        for i, image in enumerate(images):
            fname = "uploads/image" + str(i) + ".jpg"
            image.save(fname, "JPEG")
    return render_template('homepage.html')
##############################################################################

with open(os.path.join(basedir, 'result.txt'), 'r', encoding="UTF-8") as file:
    string = file.readlines()
with open(os.path.join(basedir, "relation.txt"), 'r', encoding="UTF-8") as file:
    relation = file.read()
relation = [i for i in relation.split('\n\n') if i]
with open(os.path.join(basedir, "templates/result_1.html"), "r", encoding="UTF-8") as file:
    result_1 = file.read()
with open(os.path.join(basedir, "templates/result_1_1.html"), "r", encoding="UTF-8") as file:
    result_1_1 = file.read()
with open(os.path.join(basedir, "templates/result_1_2.html"), "r", encoding="UTF-8") as file:
    result_1_2 = file.read()
with open(os.path.join(basedir, "templates/result_1_3.html"), "r", encoding="UTF-8") as file:
    result_1_3 = file.read()
with open(os.path.join(basedir, "templates/result_1_4.html"), "r", encoding="UTF-8") as file:
    result_1_4 = file.read()
with open(os.path.join(basedir, "templates/result_1_5.html"), "r", encoding="UTF-8") as file:
    result_1_5 = file.read()

utils.save_pptx_as_png("/content/drive/'Shared drives'/'BigDATA TEAM 10'/dataCampusProject-Team10/flask/outputs", "/content/drive/'Shared drives'/'BigDATA TEAM 10'/dataCampusProject-Team10/flask/slides.pptx", overwrite_folder=True)


for i in range(1, len(string)):
    result_1 += ("<div class='col-md-7'><hr><div class='row-eq-height'><div class='col-md-12' style='line-height: 40px'><p class='dark-grey-text'><mark><strong>Paragraph " + str(i) + "</strong></mark></p><a style='line-height: 40px'>")
    result_1 += string[i] # paragraph
    result_1 += result_1_1
    result_1 += ("<img src='https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/flask/slide" + str(i) + ".PNG' class='img-fluid' alt='Sample post image'>")  # ppt slide picture
    # result_1 += ("<img src='" + picture[i+1] + "' class='img-fluid' alt='Sample post image'>")
    result_1 += result_1_2
    result_1 += ("<button type='button' class='btn-outline-deep-orange' data-toggle='modal' data-target='#P" + str(i) + "'>Relation</button><div class='modal' id='P" + str(i) + "'>")  # relation tagging modal
    result_1 += result_1_3
    result_1 += relation[i-1]  # relation tagging input
    result_1 += result_1_4
result = result_1 + result_1_5
with open(os.path.join(basedir, "templates/final_result.html"), "w", encoding="UTF-8") as file:
    file.write(result)


@app.route("/result", methods=['GET', 'POST'])
def upload2():
    if request.method == 'POST':
        f = request.files.get('file')
        f.save(os.path.join(upload_dir, f.filename))
    return render_template('final_result.html')

###########################################################################################################
if __name__ == '__main__':
    app.run()
```
## HTML

### - Home Page

![home_page](images\home_page.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <title>A-Catcher</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.11.2/css/all.css">
    <!-- Bootstrap core CSS -->
    <link href="../static/css/bootstrap.min.css" rel="stylesheet">
    <!-- Material Design Bootstrap -->
    <link href="../static/css/mdb.min.css" rel="stylesheet">
    <!-- Your custom styles (optional) -->
    <link href="../static/css/style.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Do+Hyeon&family=Jua&display=swap" rel="stylesheet">
</head>

<body>

<!--Main Navigation-->
<header>

    <!-- Navbar -->
    <nav id="scroll" class="navbar fixed-top navbar-expand-lg navbar-light white scrolling-navbar">
        <div class="container" style="font-family: 'Do Hyeon',sans-serif">

            <!-- Brand -->
            <a class="navbar-brand waves-effect" href="/">
                <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/book.png"
                     width="30" height="30"
                     class="d-inline-block align-top" alt="">
                <strong class="orange-text">A-Catcher</strong>
            </a>

            <!-- Collapse -->
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                    aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <!-- Links -->
            <div class="collapse navbar-collapse" id="navbarSupportedContent">

                <!-- Left -->
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <a class="nav-link waves-effect" href="#">Home
                            <span class="sr-only">(current)</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link waves-effect" href="#AboutACatcher">About
                            A-Catcher</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link waves-effect"
                           href="#Example"
                        >Example</a>
                    </li>
                </ul>

                <!-- Right -->
                <ul class="navbar-nav nav-flex-icons">
                    <li class="nav-item">
                        <a href="https://github.com/yoonkim313/dataCampusProject-Team10"
                           class="nav-link border border-light rounded waves-effect"
                           target="_blank">
                            <i class="fab fa-github mr-2"></i>GitHub
                        </a>
                    </li>
                </ul>

            </div>

        </div>
    </nav>
    <!-- Navbar -->

</header>
<!--Main Navigation-->

<!--Main layout-->
<main class="mt-5 pt-5">
    <div class="container">

        <!--Section: Magazine v.1-->
        <div data-spy="scroll" data-target="#scroll" data-offset="0" style="font-family: 'Jua',sans-serif">
            <section class="wow fadeIn">

                <!--Section heading-->
                <h3 id="home" class="h3 text-center my-5 font-weight-bold"><img
                        src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/checkmark.jpeg"
                        width="30" height="30"
                        class="d-inline-block align-top" alt="">
                    <mark>Attention을</mark>
                    잡아
                    <mark>A+</mark>
                    를 받자!
                </h3>
                <h4 class="h4 text-muted text-center"><em>Grab both of your Attention and A+ with our
                    <mark>A-Catcher</mark>
                    !</em></h4>

            </section>
            <!--/Section: Magazine v.1-->
            <hr class="my-5">
            <section class="card wow fadeIn"
                     style="background-image: url(https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/orangeback.png);">
                <div class="card-body text-white text-center py-10 px-10 my-5 mx-5" style="font-family: 'Jua',sans-serif">

                    <h1 class="mb-3">
                        <strong>Drop your files here!</strong>
                    </h1>
                    <p>
                        <strong> A-Catcher는 PDF, JPG, JPEG, TXT, 등 다양한 형식의 파일을 지원합니다 </strong>
                    </p>
                </div>
                <head>
                    <meta charset="UTF-8">
                    <title>Flask-Dropzone</title>
                    {{ dropzone.load_css() }}
                    {{ dropzone.style('border: 3px dashed #f77300; margin: 4%; min-height: 340px; opacity:0.8;') }}
                </head>
                <body>
                {{ dropzone.create(action='upload') }}
                {{ dropzone.load_js() }}
                {{ dropzone.config() }}
                </body>
            </section>
            <hr id="AboutACatcher" class="my-5">
            <div class="container" style="font-family: 'Jua',sans-serif">

                <!--Section: Cards-->
                <section class="pt-4">

                    <!-- Heading & Description -->
                    <div class="wow fadeIn">
                        <!--Section heading-->
                        <h2 class="h1 text-center mb-5"><img
                                src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10//master/book.png"
                                width="40" height="45"
                                class="d-inline-block align-top" alt=""><em> What is
                            <mark>A-Catcher</mark>
                            ?</em></h2>
                        <!--Section description-->
                        <div class="view overlay rounded z-depth-1 mb-3">
                            <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/flask/whatis.png"
                                 class="img-fluid"
                                 alt="Sample post image">
                            <a>
                                <div class="mask rgba-white-slight"></div>
                            </a>
                        </div>

                        <ul class="text-center">

                          <strong>
                                <mark>Highlight Text</mark>
                            </strong>
                            <ul>
                                주의 집중력이 약한 사람들도 쉽게 줄글의 중심내용을 파악할 수 있도록 다양한 도형과 색상으로 텍스트를 강조
                            </ul>


                            <strong>
                                <mark>Text to PPTX</mark>
                            </strong>
                            <ul>
                                발표 대본의 제목과 소제목을 자동으로 추출하여 텍스트를 파워포인트에 삽입 </ul>
                            <ul> 텍스트 주제와 어울리는 피피티 템플릿 및 이미지 추천
                            </ul>
                        </ul>

                    </div>
                    <!-- Heading & Description -->
                </section>
            </div>
            <hr id="Example" class="my-5">
            <div class="container" style="font-family: 'Jua',sans-serif; font-size: large">

                <!--Section: Cards-->
                <section class="pt-4">

                    <!-- Heading & Description -->
                    <div class="wow fadeIn">
                        <!--Section heading-->
                        <h2 class="h1 text-center mb-5">
                            <mark>Example</mark>
                        </h2>
                        <!--Section description-->
                        <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
                            <ol class="carousel-indicators">
                                <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
                                <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
                                <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
                            </ol>
                            <div class="carousel-inner">
                                <div class="carousel-item active">
                                    <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/flask/slide%201.png"
                                         class="d-block w-100" alt="...">
                                </div>
                                <div class="carousel-item">
                                    <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/flask/slide%202.png"
                                         class="d-block w-100" alt="...">
                                </div>
                                <div class="carousel-item">
                                    <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/flask/slide%203.png"
                                         class="d-block w-100" alt="...">
                                </div>
                            </div>
                            <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button"
                               data-slide="prev">
                                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                                <span class="sr-only">Previous</span>
                            </a>
                            <a class="carousel-control-next" href="#carouselExampleIndicators" role="button"
                               data-slide="next">
                                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                                <span class="sr-only">Next</span>
                            </a>
                        </div>
                    </div>
                </section>
            </div>

        </div>
    </div>
</main>
<!--Main layout-->
<footer class="page-footer text-center font-small mdb-color darken-2 mt-4 wow fadeIn">
    <hr class="my-4">

    <!-- Social icons -->
    <div class="pb-4">

        <a href="https://github.com/yoonkim313/dataCampusProject-Team10" target="_blank">
            <i class="fab fa-github mr-3"> Visit our Github! </i>
        </a>

    </div>
    <!-- Social icons -->

    <!--Copyright-->
    <div class="footer-copyright py-3">
        © 2020 Copyright:
        <a target="_blank"> ACatcher.com </a>
    </div>
    <!--/.Copyright-->

</footer>
<!--/.Footer-->

<!-- SCRIPTS -->
<!-- JQuery -->
<script type="text/javascript" src="../static/js/jquery-3.4.1.min.js"></script>
<!-- Bootstrap tooltips -->
<script type="text/javascript" src="../static/js/popper.min.js"></script>
<!-- Bootstrap core JavaScript -->
<script type="text/javascript" src="../static/js/bootstrap.min.js"></script>
<!-- MDB core JavaScript -->
<script type="text/javascript" src="../static/js/mdb.min.js"></script>
<!-- Initializations -->
<script type="text/javascript">
    // Animations initialization
    new WOW().init();

</script>
</body>

</html>
```
### - Result Page(example 1)

![result1](images\result1.png)

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="utf-8">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.1/jquery.min.js"></script>
    <script
            src="http://code.jquery.com/ui/1.10.1/jquery-ui.min.js"
            integrity="sha256-VazP97ZCwtekAsvgPBSUwPFKdrwD3unUfSGVYrahUqU="
            crossorigin="anonymous"></script>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta http-equiv="x-ua-compatible" content="ie=edge">
    <title>A-Catcher</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.11.2/css/all.css">
    <!-- Bootstrap core CSS -->
    <link href="../static/css/bootstrap.min.css" rel="stylesheet">
    <!-- Material Design Bootstrap -->
    <link href="../static/css/mdb.min.css" rel="stylesheet">
    <!-- Your custom styles (optional) -->
    <link rel="stylesheet" type="text/css" href="../static/css/style.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Do+Hyeon&family=Jua&display=swap" rel="stylesheet">
    <style>
        #loader {
            position: absolute;
            left: 50%;
            top: 50%;
            z-index: 1;
            width: 150px;
            height: 150px;
            margin: -75px 0 0 -75px;
            border-radius: 50%;
            border-top: 16px solid yellow;
            border-right: 16px solid #FFD0F2;
            border-bottom: 16px solid orange;
            border-left: 16px solid pink;
            -webkit-animation: spin 2s linear infinite;
            animation: spin 2s linear infinite;
        }

        /* Safari */
        @-webkit-keyframes spin {
            0% {
                -webkit-transform: rotate(0deg);
            }
            100% {
                -webkit-transform: rotate(360deg);
            }
        }

        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }

        .animate-bottom {
            position: relative;
            -webkit-animation-name: animatebottom;
            -webkit-animation-duration: 1s;
            animation-name: animatebottom;
            animation-duration: 1s
        }

        @-webkit-keyframes animatebottom {
            from {
                bottom: -100px;
                opacity: 0
            }
            to {
                bottom: 0px;
                opacity: 1
            }
        }

        @keyframes animatebottom {
            from {
                bottom: -100px;
                opacity: 0
            }
            to {
                bottom: 0;
                opacity: 1
            }
        }

        #myDiv {
            display: none;
            text-align: center;
        }

        .tooltip-inner {
            background-color: #3f2363;
            max-width: 350px;
            width: 350px;
        }

        [data-placement="bottom"] + .tooltip > .tooltip-arrow {
            border-bottom-color: #3f2363;
        }
    </style>
</head>
<body>
<h2 style="top: 35%; left: 47%; text-align: center; font-family: 'Do Hyeon',sans-serif">Loading...</h2>
</body>
<body onload="myFunction()" style="margin:0;">
<div id="loader"></div>s
<div style="display:none;" id="myDiv" class="animate-bottom">
<!--Main Navigation-->
<header>

    <!-- Navbar -->
    <nav id="scroll" class="navbar fixed-top navbar-expand-lg navbar-light white scrolling-navbar">
        <div class="container" style="font-family: 'Do Hyeon',sans-serif">
            <!-- Brand -->

            <a class="navbar-brand waves-effect" href="/">
                <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/book.png"
                     width="30" height="30"
                     class="d-inline-block align-top" alt="">
                <strong class="orange-text">A-Catcher</strong>
            </a>
            <!-- Collapse -->

            <button class="navbar-toggler" type="button" data-toggle="collapse"
                    data-target="#navbarSupportedContent"
                    aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <!-- Links -->

            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <!-- Left -->
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <a class="nav-link waves-effect" href="/" target="_blank">Home
                            <span class="sr-only">(current)</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link waves-effect" href="/#AboutACatcher" target="_blank">About
                            A-Catcher</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link waves-effect"
                           href="/#Example" target="_blank"
                        >Example</a>
                    </li>
                </ul>
                <!-- Right -->
                <ul class="navbar-nav nav-flex-icons">
                    <li class="nav-item">
                        <a href="https://github.com/yoonkim313/dataCampusProject-Team10"
                           class="nav-link border border-light rounded waves-effect"
                           target="_blank">
                            <i class="fab fa-github mr-2"></i>GitHub
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <!-- Navbar -->

</header>

<!--Main Navigation-->

<!--Main layout-->
<main class="mt-5 pt-5">
    <div class="container">
        <section class="wow fadeIn">

            <!--Section heading-->
            <h2 class="h1 text-center my-5 font-weight-bold" style="font-family: 'Do Hyeon',sans-serif">
                <img src="https://raw.githubusercontent.com/yoonkim313/dataCampusProject-Team10/master/checkmark.jpeg"
                     width="30" height="40"
                     class="d-inline-block align-top" alt="">
                <mark>A-Catching Results!</mark>
            </h2>
        </section>


        <!--Grid row-->
        <div class="row text-left" style="font-family: 'Jua',sans-serif; font-size: large">
```