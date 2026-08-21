# Information disclosure on debug page

### Goal - 

Obtain and submit the `SECRET_KEY` environment variable.

### Analysis/Exploitation -

### Using free tools

When I try to avoid using features from Burp Professional, several good free tools allow for content discovery. The one I use here is [ffuf](https://github.com/ffuf/ffuf) together with the great wordlists provided by [SecLists](https://github.com/danielmiessler/SecLists).

First, I search for common directories within the web root of the application with

```bash
ffuf -w /usr/share/wordlists/SecLists-master/Discovery/Web-Content/directory-list-2.3-small.txt -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/30e0f4ad-9807-4e14-bd8f-f1a79b0171c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSTXQXXF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215622Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB1Ba8zhyljRcvCQ4BZYcIhDDnqsb6wnPdAvM%2BwCHiPvAiEAh4lq0sb66HSjEI%2FZ0fnOJ08ag9hVUoA2MCy3vG1r9MUqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGcrmTp5u%2FL78U2FzSrcA0plNGdnyl6i37ZAS0WrtSGkEJsmAOPvVbwz6pjrBheKSBN1R30FODqP2WHtd0PbyR4iqEubHtFTQa4VtBx7zpjNhpmGZjWwCjwReXWYGIuXpptVmlcZawdEpjhGLZGRCNYUlUWUL35x9esR0cwBQSmvtRV40FQncoqpYEVsQMR3HLyRUNrUx0K0REwGQC%2BoF55BVTNbHyKzqVUjXqGb4zKFz4V6T1oKd5E9kyX9XpKCNrfoPM0LIqt%2F6p2VQEka%2Fv2t6zJbithTV8O8zBjEE0Dpzq8Fe7ez12kfKxqP5u3eoXwcQeAtvLwy%2Bm7Sxr0wOvcfWafc3R2A%2FbAKpXIISo%2Bi9rSi2uVghtZC3NCec9YoQKsgqvyQA6tSks5BZX%2BV41hYD%2BHOLL4s2gZLbzhlXJHe1%2FL1S%2FmH3OjmzcXjAgMNNkNGfN4fKhe%2F%2BFycP7xuC8jO6LJAZVYJo1UzADKMsV45JmoPn8luLVyvotOLelaq8gAjloHYi0%2BWvLH7O2wfRCKCoQvhYBksWzJUj7kFydTCTgOCPdBk4rW0WnLEHgITZo7561Nw7OGIH1qXpfy%2F4qJrly6I7nOdthks3LAahNDZZhRlR316BzWJ1FFa2%2BYaE6%2FHsBzrxNgCF8wjMKWEo9QGOqUBu9ZAgJky2Z81Huo1sF1N34A%2FLlLyzjeYPg8kRogcY%2ByMxyUgscf8NFk4LAjo4bRLUKphzyvWHjlKDUHxTh7EM8FcXAbTeMtzY4leSCtA025toHnadrj39t0g6P3IdqGdqnnLurcDoHs%2BQCoNPLaSGissTqXftAreVjclhZq4RmCH851VQi53LLa6hkgWLBrki0WtOuLw8t0%2BH0fTe7TvxtUggSyW&X-Amz-Signature=4cee6eb26ac9afe8728e8a721edc866f545cf9a6c499e43db0e0438ae04beb7a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

I can now search within this directory for common files with

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery-content/Web-Content/common.txt  -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/cgi-bin/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/37effcbf-768e-40cd-9bc5-8544f17e3ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSTXQXXF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215622Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB1Ba8zhyljRcvCQ4BZYcIhDDnqsb6wnPdAvM%2BwCHiPvAiEAh4lq0sb66HSjEI%2FZ0fnOJ08ag9hVUoA2MCy3vG1r9MUqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGcrmTp5u%2FL78U2FzSrcA0plNGdnyl6i37ZAS0WrtSGkEJsmAOPvVbwz6pjrBheKSBN1R30FODqP2WHtd0PbyR4iqEubHtFTQa4VtBx7zpjNhpmGZjWwCjwReXWYGIuXpptVmlcZawdEpjhGLZGRCNYUlUWUL35x9esR0cwBQSmvtRV40FQncoqpYEVsQMR3HLyRUNrUx0K0REwGQC%2BoF55BVTNbHyKzqVUjXqGb4zKFz4V6T1oKd5E9kyX9XpKCNrfoPM0LIqt%2F6p2VQEka%2Fv2t6zJbithTV8O8zBjEE0Dpzq8Fe7ez12kfKxqP5u3eoXwcQeAtvLwy%2Bm7Sxr0wOvcfWafc3R2A%2FbAKpXIISo%2Bi9rSi2uVghtZC3NCec9YoQKsgqvyQA6tSks5BZX%2BV41hYD%2BHOLL4s2gZLbzhlXJHe1%2FL1S%2FmH3OjmzcXjAgMNNkNGfN4fKhe%2F%2BFycP7xuC8jO6LJAZVYJo1UzADKMsV45JmoPn8luLVyvotOLelaq8gAjloHYi0%2BWvLH7O2wfRCKCoQvhYBksWzJUj7kFydTCTgOCPdBk4rW0WnLEHgITZo7561Nw7OGIH1qXpfy%2F4qJrly6I7nOdthks3LAahNDZZhRlR316BzWJ1FFa2%2BYaE6%2FHsBzrxNgCF8wjMKWEo9QGOqUBu9ZAgJky2Z81Huo1sF1N34A%2FLlLyzjeYPg8kRogcY%2ByMxyUgscf8NFk4LAjo4bRLUKphzyvWHjlKDUHxTh7EM8FcXAbTeMtzY4leSCtA025toHnadrj39t0g6P3IdqGdqnnLurcDoHs%2BQCoNPLaSGissTqXftAreVjclhZq4RmCH851VQi53LLa6hkgWLBrki0WtOuLw8t0%2BH0fTe7TvxtUggSyW&X-Amz-Signature=989b7239b2e5ca13f47fcba18eac046bf9b54c6907172cce60eb487c4191d65e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Using Burp Professional

Go to the "Target" > "Site Map" tab. Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to `/cgi-bin/phpinfo.php`.

or Use the default options and start the content discovery. Burp quickly shows the `phpinfo.php` file in the site map:

Opening this file in the browser and scrolling through the content shows the answer:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ebc3c145-2e85-4bdd-86c9-badcaff70ec6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSTXQXXF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215622Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB1Ba8zhyljRcvCQ4BZYcIhDDnqsb6wnPdAvM%2BwCHiPvAiEAh4lq0sb66HSjEI%2FZ0fnOJ08ag9hVUoA2MCy3vG1r9MUqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGcrmTp5u%2FL78U2FzSrcA0plNGdnyl6i37ZAS0WrtSGkEJsmAOPvVbwz6pjrBheKSBN1R30FODqP2WHtd0PbyR4iqEubHtFTQa4VtBx7zpjNhpmGZjWwCjwReXWYGIuXpptVmlcZawdEpjhGLZGRCNYUlUWUL35x9esR0cwBQSmvtRV40FQncoqpYEVsQMR3HLyRUNrUx0K0REwGQC%2BoF55BVTNbHyKzqVUjXqGb4zKFz4V6T1oKd5E9kyX9XpKCNrfoPM0LIqt%2F6p2VQEka%2Fv2t6zJbithTV8O8zBjEE0Dpzq8Fe7ez12kfKxqP5u3eoXwcQeAtvLwy%2Bm7Sxr0wOvcfWafc3R2A%2FbAKpXIISo%2Bi9rSi2uVghtZC3NCec9YoQKsgqvyQA6tSks5BZX%2BV41hYD%2BHOLL4s2gZLbzhlXJHe1%2FL1S%2FmH3OjmzcXjAgMNNkNGfN4fKhe%2F%2BFycP7xuC8jO6LJAZVYJo1UzADKMsV45JmoPn8luLVyvotOLelaq8gAjloHYi0%2BWvLH7O2wfRCKCoQvhYBksWzJUj7kFydTCTgOCPdBk4rW0WnLEHgITZo7561Nw7OGIH1qXpfy%2F4qJrly6I7nOdthks3LAahNDZZhRlR316BzWJ1FFa2%2BYaE6%2FHsBzrxNgCF8wjMKWEo9QGOqUBu9ZAgJky2Z81Huo1sF1N34A%2FLlLyzjeYPg8kRogcY%2ByMxyUgscf8NFk4LAjo4bRLUKphzyvWHjlKDUHxTh7EM8FcXAbTeMtzY4leSCtA025toHnadrj39t0g6P3IdqGdqnnLurcDoHs%2BQCoNPLaSGissTqXftAreVjclhZq4RmCH851VQi53LLa6hkgWLBrki0WtOuLw8t0%2BH0fTe7TvxtUggSyW&X-Amz-Signature=dbbee3cd3da1497bf3f605ea2fbdf138e8deb0e3a8be13d3b286cad72b1a3a3b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
