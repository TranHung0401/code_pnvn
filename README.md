# code_pnvn

1/ Smooth Scrolling
2/ Menu fix
3/ Number animated
4/ Lấy thứ ngày tháng năm
5/ Addthis
6/ FormatNumber
7/ google transfer
8/ Water mark
9/ Get param URL
10/ Đổi màu chữ
11/ Lấy value form

1/ Smooth Scrolling
<script>
    $(document).ready(function() {
        $('.menu ul li a').click(function() {
            const id = $(this).data('id');
            $('html, body').animate({
                scrollTop: $('.' + id).offset().top
            }, 500);
        });
    });
</script>

2/ Menu fix
<script>
    $(window).scroll(function() {
        const heightmenu = $('#header').height();
        if ($(window).scrollTop() > heightmenu) {
            $('#header').addClass('menufix');
        } else {
            $('#header').removeClass('menufix');
        }

    });
</script>

3/ Number animated
<script>
    var isAlreadyRun = false;
    $(window).scroll(function() {
        var bottom_of_window = $(window).scrollTop() + $(window).height();
        var bottom_of_object = $('.thongso').position().top;

        if (bottom_of_object - bottom_of_window < 50) {
            if (!isAlreadyRun) {
                $('.tso-number span').each(function() {
                    $(this).prop('Counter', 0).animate({
                        Counter: $(this).text()
                    }, {
                        duration: 4000,
                        easing: 'swing',
                        step: function(now) {
                            $(this).text(Math.ceil(now));
                        }
                    });
                });
            }
            isAlreadyRun = true;
        }

    });
</script>

4/ Lấy thứ ngày tháng năm
<?php
function getThu($dmy)
{
    date_default_timezone_set('Asia/Ho_Chi_Minh');
    $weekday = date($dmy);
    $weekday = strtolower($weekday);
    switch ($weekday) {
        case 'monday':
            $weekday = 'Thứ hai';
            break;
        case 'tuesday':
            $weekday = 'Thứ ba';
            break;
        case 'wednesday':
            $weekday = 'Thứ tư';
            break;
        case 'thursday':
            $weekday = 'Thứ năm';
            break;
        case 'friday':
            $weekday = 'Thứ sáu';
            break;
        case 'saturday':
            $weekday = 'Thứ bảy';
            break;
        default:
            $weekday = 'Chủ nhật';
            break;
    }
    return $weekday . ', ' . date('d/m/Y ');
}

?>

5/ Addthis

<div class="list-addthis" style="border:none">
    <div style="display:flex;width: 100%;margin-bottom: 10px;margin-top:10px;">
        <script type="text/javascript">
            var addthis_config = {
                "data_track_addressbar": true
            };
        </script>
        <script type="text/javascript" src="//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-51d3c996345f1d03" async="async"></script>
        <script type="text/javascript">
            var addthis_config = {
                data_track_clickback: false,
            }
            var addthis_share = {
                templates: {
                    twitter: "{{title}} {{url}} via @YourTwitterName"
                }
            }
        </script>
        <div class="zalo-share-button" data-href="<?= $ctsp[0]['alias_' . $lang] ?>.html" data-oaid="579745863508352884" data-layout="1" data-color="blue" data-customize=false></div>&nbsp;
        <script src="https://sp.zalo.me/plugins/sdk.js"></script>
        <script>
            (function(d, s, id) {
                var js, fjs = d.getElementsByTagName(s)[0];
                if (d.getElementById(id)) {
                    return;
                }
                js = d.createElement(s);
                js.id = id;
                js.onload = function() {};
                js.src = "https://sp.zalo.me/plugins/sdk.js";
                fjs.parentNode.insertBefore(js, fjs);
            }(document, 'script', 'zalo-jssdk'));
        </script>
        <div class="addthis_native_toolbox"></div>
    </div>
</div>

6/ FormatNumber

<script>
    function formatNumber(nStr, decSeperate, groupSeperate) {
        nStr += '';
        x = nStr.split(decSeperate);
        x1 = x[0];
        x2 = x.length > 1 ? '.' + x[1] : '';
        var rgx = /(\d+)(\d{3})/;
        while (rgx.test(x1)) {
            x1 = x1.replace(rgx, '$1' + groupSeperate + '$2');
        }
        return x1 + x2;
    }

    vidu: formatNumber(pricePromotionPriceNew, ',', '.');
</script>

7/ google transfer
<script type='text/javascript' src='templates/js/flags.js'></script>
<script type="text/javascript">
    function GoogleLanguageTranslatorInit() {
        new google.translate.TranslateElement({
            pageLanguage: 'vi',
            autoDisplay: false
        }, 'google_language_translator');
    }
</script>
<script type="text/javascript" src="http://translate.google.com/translate_a/element.js?cb=GoogleLanguageTranslatorInit"></script>

<div id="lang_top">
    <div class="langSite">
        <a href="javascript:void(0)" onclick="doGoogleLanguageTranslator('vi|vi'); return false;" title="Việt nam" class="flag vi"><img src="templates/images/vi.png" alt="Vi"></a>
        <a href="javascript:void(0)" onclick="doGoogleLanguageTranslator('vi|en'); return false;" title="English" class="flag en"><img src="templates/images/us.png" alt="En"></a>
    </div>
    <div id="google_language_translator"></div>
</div>

<style>
    body {
        top: 0 !important;
    }

    #google_language_translator,
    .skiptranslate {
        display: none;
    }
</style>

8/ Water mark
<?php

$hinh_anh = addslashes($_POST['hinh_anh']);
$hinh_anh_watermask = rand(0, 9999) . "-" . basename($_POST['hinh_anh']);
//Create watermark
$file_hinh = "../img_data/images/" . $_POST['hinh_anh'] . "";
$imgdongdau = "img/logowatermask.png";
$destination = "../img_data/watermark/" . $hinh_anh_watermask . "";
watermark_image($file_hinh, $destination, $imgdongdau, 50, 50);

function watermark_image($file, $destination, $overlay, $X, $Y)
{
    $watermark =    imagecreatefrompng($overlay);
    $wtsize = getimagesize($overlay);
    $wtsize_x = $wtsize[0];
    $wtsize_y = $wtsize[1];
    $source = getimagesize($file);
    $source_mime = $source['mime'];
    $source_x = $source[0];
    $source_y = $source[1];

    $left = ($source_x * $X / 100) - $wtsize_x / 2;
    $right = ($source_y * $Y / 100) - $wtsize_y / 2;

    if ($source_mime == "image/png") {
        $image = imagecreatefrompng($file);
    } else if ($source_mime == "image/jpeg") {
        $image = imagecreatefromjpeg($file);
    } else if ($source_mime == "image/gif") {
        $image = imagecreatefromgif($file);
    }
    imagecopy($image, $watermark, $left, $right, 0, 0, imagesx($watermark), imagesy($watermark));
    imagepng($image, $destination);
    return $destination;
}

$data['watermask'] = $hinh_anh_watermask;

?>

9/ Get param URL

<?php
function getSearch()
{
    $link = explode("?", $_SERVER['REQUEST_URI']);
    if ($link[1] != '') {
        $vari = explode("&", $link[1]);
        $search = array();
        foreach ($vari as $item) {
            $str = explode("=", $item);
            $search["$str[0]"] = urldecode(addslashes($str[1]));
        }
    }
    return $search;
}
?>

10/ Đổi màu chữ
<script>
    $(document).ready(function() {
        var elements = $('.colortext'); // Lấy tất cả các phần tử có class là "colortext"

        // Lặp qua từng phần tử và thực hiện các thao tác bạn mong muốn
        elements.each(function() {
            var text = $(this).text(); // Lấy nội dung của từng phần tử
            let character = $(this).data('character');
            var firstTwoWords = text.split(' ').slice(0, character).join(' '); // Lấy hai từ đầu tiên trong chuỗi

            // Đổi màu cho hai từ đầu tiên
            var coloredText = '<span style="color: #005ba3;">' + firstTwoWords + '</span>' + text.substr(firstTwoWords.length);

            // Gán nội dung mới cho phần tử
            $(this).html(coloredText);
        });
    });
</script>

11/ Lấy value form
<script>
    var dataArray = $(this).serializeArray(),
        dataObj = {};
    $(dataArray).each(function(i, field) {
        dataObj[field.name] = field.value;
    });
</script>
