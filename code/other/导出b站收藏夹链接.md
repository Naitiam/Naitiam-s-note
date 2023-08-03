控制台粘贴以下代码

```
function get_list () {
    var result = "";
    $(".fav-video-list > li >a.title").each(function(){
        var title = $(this).text();
        var link = "https:" + $(this).attr("href");
        result += '<DT><A HREF="' + link + '" ADD_DATE="' + Date.now() + '" LAST_MODIFIED="' + Date.now() + '" ICON_URI="' + link + '" ICON="' + link + '">' + title + '</A>\n';
    });
    return result;
}
 
var html = '<!DOCTYPE NETSCAPE-Bookmark-file-1>\n<!-- This is an automatically generated file.\n     It will be read and overwritten.\n     DO NOT EDIT! -->\n<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=UTF-8">\n<TITLE>Bookmarks</TITLE>\n<H1>Bookmarks</H1>\n<DL><p>\n';
 
function main (){
    html += get_list();
    if($(".be-pager-next:visible").length == 0) {
        html += '</DL><p>\n';
        download('bookmarks.html', html);
        return;
    } else {
        $(".be-pager-next").click();
        setTimeout(main, 500);
    }
}
 
function download(filename, text) {
    var element = document.createElement('a');
    element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
    element.setAttribute('download', filename);
    element.style.display = 'none';
    document.body.appendChild(element);
    element.click();
    document.body.removeChild(element);
}
 
main();