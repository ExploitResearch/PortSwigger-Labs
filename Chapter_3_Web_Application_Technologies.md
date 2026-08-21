# Chapter 3 Web Application Technologies

# HTTP Hypertext Transfer Protocol

- **Connectionless protocol**
  - **Client sends an HTTP request to a Web server**
  - **Gets an HTTP response**
  - **No session formed, nothing remembered--no "state"**
## HTTP Requests

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb91b3ab-c66e-4c39-a64e-80f747aebcef/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=6fc1e59375c5a47ff441ea5422533dfcf9a433f334d87c148817bd0a3591459b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Verb: GET (also called "method")**
- **URL: /css?family=Roboto:400,700**
  - **Portion after ? is the *****query string***** containing Parameters**
- **Version: HTTP/1.1**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb91b3ab-c66e-4c39-a64e-80f747aebcef/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=6fc1e59375c5a47ff441ea5422533dfcf9a433f334d87c148817bd0a3591459b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Referer: URL the request originated from**
- **User-Agent: browser being used**
- **Host: Hostname of the server**
  - **Essential when multiple hosts run on the same IP**
  - **Required in HTTP/1.1**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ab52d9f2-c47b-4f0b-8218-fa40af8a11e0/image3.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=f45b159af5b9b6ac2a9efef42ebca14df5c20787673aca78cebb87836deab039&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Cookie: additional parameters the server has issued to the client**
## HTTP Response

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e89cf121-b1e9-4ac3-86bc-fee1613533c9/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=11b9e93ebaedaee047d56693b6a89c76aa678af2ef8e945b9baf01b4a537a20e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **First line**
  - **HTTP version**
  - **Status code (200 in this case)**
  - **Textual "reason phrase" describing the response**
    - **Ignored by browser**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6b2eaa2c-29fd-4f94-a178-1ad3fbcc26d1/image5.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=8b461da24ddd9a7fb96b6b5f372348af3a432a5f947f2e8d0c43381a413334e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Server: banner of server software**
  - **Not always accurate**
- **Set-Cookie used to set cookie values**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/79cb5f82-ca96-44f0-b958-dd3c2e27527d/image6.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=34d90eb344770ba199dc0870ffae6b025276309b78578bff65dac728a5204ec4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Pragma: tells browser not to store response in its cache**
- **Expires: set to a date in the past to ensure that the content is freshly loaded**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e89cf121-b1e9-4ac3-86bc-fee1613533c9/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=11b9e93ebaedaee047d56693b6a89c76aa678af2ef8e945b9baf01b4a537a20e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Message Body after header contains data of type specified in Content-Type header**
## HTTP Methods: 

1. **GET**
  - **GET retrieves resources**
    - **Can send parameters in the URL query string**
    - **Users can bookmark the whole URL**
    - **Whole URL may appear in server logs and in Referer headers**
    - **Also on the browser's screen**
  - **Don't put sensitive information in the query string**
1. **POST**
  - **POST performs actions**
  - **Request parameters can be in URL query string and in the body of the message**
    - **Parameters in body aren't saved in bookmarks or most server logs**
    - **A better place for sensitive data**
  - **POST requests perform actions, like buying something**
  - **Clicking the browser's Back button displays a box like this**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b4a3b17c-20e5-4d77-90be-11be5e6e3719/image7.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666AHNDHY2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204515Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIF5uQp9cT7lwUCu8mqtAJKGqZIJrH06esqBSwY9aKchMAiADtZc6ZBY7VcOXakW8MdT2VRPHAlIJYyYdyTIxj53heSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMnrQaYuzWpK5Xm01lKtwDKi51dkjmzVDVga1HZ79Tm13s7%2FS2Eve9cFNMdV7AV8vDKFbubQwQIZhWTrrntZPGx%2B2sQ%2F2JkDdN3b35%2BrkYJzZ%2BeE49b200S3QMClxGZfnsEZro0L9YZ1eySHB9dDmXWgxW9RajM8L8MkIJfYFWThxmv51gDjs4TkUTdDGHVQaQK%2BrDJnIpHIJB2DQi1ixJIcEMFfbqdpuRSJXyXeZGm1TP%2FdbDrFF5LJdXRkYeap7pxzOL37%2BATzuYPGGky2YKqhLsH6b4KwdjAAxFhF%2BdFkKzZgDUfq0U0P4DYll0%2FgpY9CkJew7%2FzF4%2Bjp63tykShAgN8MqAnxKCygOKIxDWYS5xzxQUP%2FS1luLTbER%2BzimCPM1fQr4Tkow7hicO%2FyeZQGM9AC%2FEI0FbAt2Uhw6KMQB87QQjtErISfw8%2B921Hls71hE4PpSOyJbJ5j1EeCaGQMvndCNsncASKTMSgs3SwKvq9viUlBLV9JSl6z6pkCrmUiVsLVmWgQY0G7BEgJSubnCHN500DhOUePlihjfzn1cVHllyYYcoU%2BXeFZ3Mj%2FjZT90xPnejqSqtYGRZu1GYBRldMU4Q7DbZ%2F3AWJrqyNGR%2Bc5jWMsG2IjntfmgsRIQEoJELhyiug8UuRPowncai1AY6pgGstp%2FGdoNbsIpi5HiQxc%2BseLmLCz0YlhD%2BIC%2F8Gik%2BOaqGNzTvG0jhqTjhRKsBI8duHB%2FPoDBfdVOn%2Ffo6%2FYv4e%2FdbYNEswGzO3DW9a9sjSMqix%2BXfcU%2Fzdi2lv10nzwI8VXPJcSUixofox4Gyzaa9E6si4ci%2B3Tu%2BE8Dw1ysqekZ8nIE7EvMe2Hs257qtjlzK73R9tw6OUjvanY6Mp2MlZ47eISF6&X-Amz-Signature=6a877dacde2b19aeade049818c15e0535cfeef45cd5bf851d7efdaa1cd1ab2b6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

1. **Other HTTP Methods**
  - **HEAD returns only the header, not the body**
    - **Can be used to check if a resource is available before Geting it**
  - **OPTIONS shows allowed methods**
  - **PUT uploads to server (usually disabled)**
## URL (Uniform Resource Locator)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1b7e9970-7b89-4d5f-8bfb-97b319b883ce/image8.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=f105f9ac1dc793bc2965ce927a1d14b8f81550cfea28c46fec47abce24e00f63&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **If protocol is absent, it defaults to HTTP**
- **If port is absent, it uses the default port for the protocol**
  - **80 for HTTP, 443 for HTTPS, etc.**
## REST (Representational State Transfer)

- **RESTful URLs put parameters in the URL, not the query string**
- http: [//wahh-app.com/search?make=ford&model=pinto](https://wahh-app.com/search?make=ford&model=pinto) **becomes 
**http: [//wahh-app.com/search/ford/pinto](https://wahh-app.com/search/ford/pinto)
## HTTP Headers

### General Headers

- connection tells the other end of the communication whether it should close the TCP connection after the HTTP transmission has completed or keep it open for further messages.
- content-Encoding specifies what kind of encoding is being used for the content contained in the message body, such as gzip, which is used by some applications to compress responses for faster transmission.
- content-Length specifies the length of the message body, in bytes ( except in the case of responses to HEAD requests, when it indicates the length of the body in the response to the corresponding GET request).
- content-Type specifies the type of content contained in the message body, such as text/html for HTML documents.
- Transfer-Encoding specifies any encoding that was performed on the message body to facilitate its transfer over HTTP. It is normally used to specify chunked encoding when this is employed.
### **Request Headers**

- Accept tells the server what kinds of content the client is willing to accept, such as image types, office document formats, and so on.
- Accept-Encoding tells the server what kinds of content encoding the client is willing to accept.
- Authorization submits credentials to the server for one of the built-in *HTTP* authentication types.
- cookie submits cookies to the server that the server previously issued.
- Host specifies the hostname that appeared in the full URL being requested.
- If-Modified-Since specifies when the browser last received the requested resource. If the resource has not changed since that time, the server may instruct the client to use its cached copy, using a response with status code 304.
- If-None-Match specifies an *entity tag,* which is an identifier denoting the contents of the message body. The browser submits the entity tag that the server issued with the requested resource when it was last received. The server can use the entity tag to determine whether the browser may use its cached copy of the resource.
- origin is used in cross-domain Ajax requests to indicate the domain from which the request originated (see Chapter 13).
- Referer specifies the URL from which the current request originated.
- user-Agent provides information about the browser or other client software that generated the request.
### **Response Headers**

- Access-Control-Allow-Origin indicates whether the resource can be retrieved via cross-domain Ajax.
- cache-Control passes caching directives to the browser (for example, no-cache).
- ETag specifies an entity tag. Clients can submit this identifier in future requests for the same resource in the If-None-Match header to notify the server which version of the resource the browser currently holds in its cache.
- Expires tells the browser for how long the contents of the message body are valid. The browser may use the cached copy of this resource until this time.
- Location is used in redirection responses (those that have a status code starting with 3) to specify the target of the redirect.
- Pragma passes caching directives to the browser (for example, no-cache).
- server provides information about the web server software being used.
- set-cookie issues cookies to the browser that it will submit back to the server in subsequent requests.
- WWW-Authenticate is used in responses that have a 401 status code to provide details on the type(s) of authentication that the server supports.
- X-Frame-Options indicates whether and how the current response may be loaded within a browser frame (see Chapter 13).
## Cookies

- **Cookies are resubmitted in each request to the same domain**
  - **Unlike other request parameters, such as the query string**
A server issues a cookie using the Set-Cookie response header, as you have seen:

```javascript
Set-Cookie: tracking=tI8rk7joMx44S2Uu85nSWc
```

The user's browser then automatically adds the following header to subsequent requests back to the same server:

```javascript
Cookie: tracking=tI8rk7joMx44S2Uu85nSWc
```

### Set-Cookie Header

- **path - URL path for which the cookie is valid**
- **secure - transmit cookie only via HTTPS**
- **HttpOnly - Cookie cannot be directly accessed via client-side JavaScript**
Optional attributes

  - **expires - date when the cookie stops being valid**
    - **If absent, cookie is used only in the current browser session**
  - **domain - specified domain for which cookie is valid**
    - **Must be the same or a parent of the domain from which the cookie is received**
    - **"Same-Origin Policy"**
## Status Codes Groups

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5688e6c6-70d2-427b-b4b1-74b17472b5e0/image14.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204512Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=909f043feea7c169c6bf714781827fc0a919601232eebaff553e0f27008f6dd2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Important Status Codes

- **200 OK - request succeeded, response body contains result**
- **301 Moved Permanently - redirects the browser, client should use new URL in the future**
- **302 Found - redirects browser temporarily. Client should revert to original URL in subsequent requests**
- **304 Not Modified - browser should use cached copy of resource**
- **400 Bad Request - invalid HTTP request**
- **401 Unauthorized - Server requires HTTP authentication.**
  - **WWW-Authenticate header specifies the type(s) of authentication supported**
- **403 Forbidden - no one is allowed to access resource, regardless of authentication**
- **404 Not Found - requested resource does not exist**
- **500 Internal Server Error - unhanded exception in an app, such as a PHP error**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d7d16957-c053-4e73-b1cd-9a096be62c1b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WCTCHF3K%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204519Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHNPCKzcgG4YB%2BdSsNUiWs7jDQGGQm9R2FWylJ641h1%2FAiEAhR5IPn%2FKhctmzJHmAu7kmO%2Bgnkl4BFlNTl89oEtMFeoqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNw415UM6p7Na1d0USrcA3CnSJUMS6fhaUWopJGtCyIzaejZ7jh61A0Qdl3Vt%2BtQfBVztNIlMYg9U%2B9ONn5lt2LQ3LJbn1Zwka8DdfmwX3XZmujFiPX45vEKgsZrtCAoAs2Nxmj30QXdrRW2f3UvBU2Uc%2BZqZpcm2WSFJZnOECs41lA9poRjSWtnlWfUtCy%2FAV0EESNVBO9vGpRZNxfNWOCWtt9NIVBLWsYYVsWiIS2baVcwdvgT3SAqK%2Bgb5Yr0oxzNZao2FlG01%2BGGbzDZQXXlQOdcB51lZgOUsaQsw2O1yHu6bLbZ9TCjGx%2FwVjgueMF43c%2Fsya9RmwfnmBUgUpSlhTS0oy%2FDnSjAqaLqk5siuW84nKVd0E2btE4OExBRcAbkg0iEg8nKGLdsZCgMp0OmOEVN3rjAAmLJyOIU9O7jwTzHTh1WwnnX3QCIXDuVOgAuQst6TtR20g%2Ffyo721%2FmtVqqC1ZIwf7c1%2BgvKQZ7Aic8%2ByoGkshJ4GKWlm3wkENsews8VjraR2HRaSU8TyG1hOve4GflHIu4UN1mDvRVgzhM4pTWrwb54VNkG70HfJsomVp0YAoLib%2BYUAStlm55H5%2F4BuyE0ul5dZNM4VxNeZPrya3r1YKJEI1rFNkGLaKpQXMkiaCeWmYuXMNTIotQGOqUBRxZ%2BzG5f41AJsQTlGSNwT8HavEOQ%2FnDsE7c5Vqmmhk%2FqoYDLgjYVN7BSjkKgSZQ4Q8q2nuOBTdXs5KYDWCp1yiTBo1QlaEpQGkVp4A%2BivUVHmFGynbKh7IiNRX8D54XbQKV3thz%2BBuAkgfmIN2A1K5BnDyr8p6YeFkAcYk5phtafbYu0g2gwJYdw1%2FJeGuQ2SRWv%2BMPDk1S7zz%2Fls0TXtgFA3LkD&X-Amz-Signature=5e4273ea5e3a98e379e47622f6f76b32f810196bb2dad11e9e97f24bf7e778ba&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2ff60443-f464-450e-b840-ffb4d201d32e/image16.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QWDVY4Z6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204519Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDf%2Bv2MmQ7EVoVbZ8yiEkD8WWztOwfjAbwltgQU58MkWwIgG2IsJb3QITl8xN0IJ6MNPtuvasat3pbtkkXlcjC9x4MqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDH9NnR2rcYAlyuztvCrcA2jXWqoKABG7SzdnZ81LWRODAOtyV5p9GUskigghH%2F9ElRPqzs8UB6HMhIhKP2FgCFbvJeUEQyixIxX3TZfXuTNJnkr9HmIxAEkrzlvlbINGZHCMLmOlnJeBk3MbkjFcgljWoyRSMTt4ScPfBUQJnpYxet7lJWTAUDOZUjrhc5NZWS%2F5n4pN27i3hcEko0gcNuApjleSDwlV%2BM8o6zSbIXmjrN00dg5XbZEf0pxY5Q%2FPboYnOmh%2BcmeaWNGsA4HaP0ZOV4JbL%2FMYfA2TN39hXqSnmYBr9N4FrwDh5acfIAb5NU3iyxUTJsvnMRWZtDNBoWf7HKhglXi9jzs%2B7J6X3EC285QF4wQbSowiWflp5nT4YAZ%2FC8wHmgJ8My1WvOoceVeWzUEgN40GaFLvd5xN7%2FNlFhqyvaiCR8bv%2F1%2BzqDiRKahQiAAwnXEk7L5ogLWa0WFJaovj5xRJ1eaaKArQ12icgzI7nYO4zD3BlmSaytpCTTVlW5l8kUbiYuoXMCZXo70hSc8iXC8w4bU2oxEI98wg1bYngOdLTJiUbCx0oYJcZReCV7nivLxkUPHXMXcWTHnGlIzqWeOvzx0W3MD30M%2Fk%2FuTySW9AiTIFUdzz4LpS24eUnZSis9e9RdlcMKTGotQGOqUBTqpH4%2FmdmR0W7xO%2FS6lzSBTtbHluYCG%2BwKD8YTFoPENT1mem5Jd2h4q5uGCygOnn%2BJjmXcDGgPr8UOF7FmTjOCZoE3Wga866%2FyAFhR2EkocHD5%2B8oeW3GxQhWnuYbhE1HGJQFJQKaiRssRh9ZyTCFoIEN%2BST7fsmmr9TF5cHhc2NK645Ao0FnAY6gN3XrJre1E%2BO5PKe2IyH1m7KJLDMNMjaaz0%2F&X-Amz-Signature=00c7124833e9d15600c9925019e48aaffc31b05d87df38f4e768291445ca237a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc284b6a-7782-4e59-a0a7-204729e55c22/image17.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SFKWLMGA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204520Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID4Ol6PvVkxho5yrR28AqaGJ3NLwWNAjJIPOopQPJEtNAiAZH%2FTkjxpzUDdlOIBia1mjwk0V1QppxEl1MxZiM6yHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlkmY060NUbH%2FmsAKKtwDBK7yoPfXa7BavYOC0Aidz%2BPPP4Q8kR%2Bgf%2F8T%2FzulrXQ5gu20guVCvAuLgZTgvgK2t9UeEpwrdhN7VgTRMkafrR7i25LAGV2DLXYEQs70lX4CvtF5LaWuPG0PNFh%2Fji8EMuYcttfe5bw%2B%2BkJwxk5yBJclN1Y2OpTxT1lbKCOTIWe1O2vHlayi%2BH4zWmhtxPUedMM2QoKGbvE%2FPtGBGzqhevPvEaRn%2FgBAmECXV4VevgPIB4BpFTr%2B%2BTGK2nBCIS%2F8CghqWm266RkZV1%2FxY29CJ9y52yepLm35pVWTqz6vfRMpKKIB7ftJxFH%2FkClrgplrQqkOoj%2BETEUWitnvlbP29tHnPDlSxJ6Vo2bApHoUbcpWTIyr%2FxSuDLfDn7GxIwK9fEOuzOKIPlPMsfzxfW0KJLr9s%2FPN5PCGX6vE4uoeLO7pF9xMVP5pWI8Wq0I0D2djLU4RfpzA8JqeIptvCC%2BdBwwwoNil6hqI4ujk5S8t57nlSg0kpfQUKjHFEopNRpbnVRSqS%2FaXNxO5SvATNKZfHThOe9Ebmck8br%2F35vZtdRWkvcX8WoSCod6YfNsPuiXwoFtSsqQ56Eg0KnR%2FqqbZqgZedAk1VdGp9Yv8Vb4ayz94LpLusxxg0PXRhnEwiMai1AY6pgFt6msCo7YU%2B4RUObsv74ZlbHcbvhwAUJEEZcUZiAqFUN0dffZ0LfzbHViaZ3RH2tOxNIiB7yunYLxNzDFk5FCmroF9111wR4tq6ITV9Yhqg%2FXghpkQlo08TkETSVq1%2BEIZf7eZEoFFxtcGN5hBoYq0rskLmoNAlVxSukSjn5CLnmgEdVnVnQ9K6LzYuAOO4%2Fje1hpFxZo%2BMVt3sXk7rD0NH3oyRfwW&X-Amz-Signature=cd5964057f4b02b2d6440953b72656546f570b52101c5de83615494a276218bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ecc2cee-896d-4013-89cd-6c18309d5a09/image18.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZIV6H6S%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204520Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDLrM4%2FtSnQt0pMHJuDyjG5sn0z5Ne2PSF1YbxX8VkxLgIgTdA8cR%2BioCMYKI9Xn35GLUoXaJlJ58BdBxn7tDhcVE0qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDH7K3jxWl2%2B5zfHhRSrcA7WoaXdLWvUCU4B3llniO8Mt2fSv6CDC9ULr17%2BHCxXpjqUm2mgtUXEX3Cupz03jbwi47f8SIRhgCmXgMmVBQ6ooyg%2FpryQPKWCtxUM96e7gtsSRRDn0SZ7%2Bl9fNf0mbI1%2FQFcCg6fdY72e%2Bu%2FFlHrNzX%2FBKEPCt071eTG9xQIte%2FkCTMvuOfgWbxzQXy64BP5aM34JQBvsVBZKUTcvEV2nGlYhe7diBIzOFxlM8FZUbKj3kBAWlRn%2FqEDN13AtOU9n2WQVzi40m97CbKZLvMxW1%2FEKf%2F0xTJLD4HQcQ2ccki7%2BqmUELFW8yPCDfMbQL%2BBrH8CHttCaiYp2J4WpU6FgpMZn89WM%2BrVZCQ4%2F6Z2AyVaDoL4TmJf9Gw6WEkrRN%2F3QGC47KNfjYOJ6iapwAHcHlIpuLLRdQ4Hqp%2BHHC1hE5xBszcamyr4Sf9Ira8nw4vPRqOrpNXustUtlWb0%2By4aF1u%2B2tm4xiyLewoSIA5RCJxD1%2F331l3Cn6WKbe1SMPJ598BoWg383kH%2B75JPrGsynkxbdok9AyrcVXKUhkt2Px0SJ8INWapfG4IdNQT9V2QkrYOlpy3vm93xCUKUsjrEIPnEGJmnZLMWP%2B%2FeqNhb0Ss5YCEIB25sfqMJUzMJDJotQGOqUBIijBB9hKrSkZq%2FldCdsfoLuYX5tO%2FfI31XzsVE0A9dcbrcC4ZTubAhLyhyEnGngMMaeM%2BnUrVUFMCgNUsO5aPyamxwlOjfaEcLNm3rzNRGn5SOTmGMmV0tyORyR%2BkhzqpJC8OTgOqwtcEVthnFxTxq31ORJhf29RGq2sW6uaRrV6khvxIXzH5bd1TNMLdVNBdprGmWwi7NGiHAKB1y4HBMXkusx4&X-Amz-Signature=9abd786565190b57823338ff3d3478d558693aa5a80b034ad83cbfd445d6c9cc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## HTTPS

- **HTTP over SSL (Secure Sockets Layer)**
  - **Actually now TLS (Transport Layer Security)**
  - **All versions of SSL are deprecated**
  - **Protects data with encryption**
  - **Protects data in motion, but not at rest or in use**
## HTTP Proxies

- **Browser sends requests to proxy server**
- **Proxy fetches resource and sends it to browser**
- **Proxies may provide caching, authentication, and access control**
### HTTPS and Man-in-the-Middle (MITM) Attacks

- **HTTPS connections use public-key cryptography and end-to-end encryption**
  - **Only the endpoints can decrypt traffic**
- **Companies wishing to restrict HTTPS traffic have two choices**
  - **Perform complete MITM with fake certificates, or real root certificates from trusted CA's**
  - **Allow encrypted traffic to trusted domains without being able to inspect it**
### HTTPS and Proxies

- **Browser sends an HTTP request to the proxy using the CONNECT method and destination hostname and port number**
- **If proxy allows the request, it returns 200 status and keeps the TCP connection open**
- **Thereafter acts as a pure TCP-level relay to the destination web server**
## HTTP Authentication

- **Basic: sends username and password in Base64-encoding**
- **NTLM: Uses Windows NTLM protocol (MD4 hashing)**
- **Digest: Challenge-response using MD5 hashing**
- **These are generally used in intranets, not on the Internet**
- **All are very weak cryptographically, and should be protected with HTTPS**
# Web Functionality

## Server-Side Functionality

- **Static content - HTML pages and images that are the same for all users**
- **Dynamic content - response created in the fly, can be customized for each user**
  - **Created by scripts on the server**
  - **Customized based on parameters in the request**
When a user’s browser requests a dynamic resource, normally it does not simply ask for a copy of that resource. In general, it also submits various parameters along with its request. It is these parameters that enable the server side application to generate content that is tailored to the individual user.

**HTTP requests can be used to send parameters to the application in three main ways:**

1. **HTTP Parameters****
**May be sent in these ways:
  1. In the URL query string
  1. In the file path of REST-style URLs
  1. In HTTP cookies
  1. In the body of requests using the post method
1. **Other Inputs**
- **Server-side application may use any part of the HTTP request as an input**
  - Such as User-Agent
  - Often used to display smartphone-friendly versions of pages
1. **Web Application Technologies**
  1. Scripting languages such as PHP, VBScript, and Perl
  1. Web application platforms such as [ASP.NET](http://asp.net/) and Java
  1. Web servers such as Apache, IIS, and Netscape Enterprise
  1. Databases such as MS-SQL, Oracle, and MySQL
  1. Other back-end components such as filesystems, SOAP-based web services, and directory services
### **The Java Platform**

- **Standard for large-scale enterprise applications**
- **Lends itself to multitiered and load-balanced architectures**
- **Well-suited to modular development and code reuse**
- **Runs on Windows, Linux, and Solaris**
### **Java Platform Terms**

- **Enterprise Java Bean (EJB)**
  - Heavyweight software component to encapsulate business logic, such as transactional integrity
- **Plain Old Java Object (POJO)**
  - User-defined, lightweight object, distinct from a special object such as an EJB
- **Java Servlet**
  - Object on an application server that receives HTTP requests from client and returns HTTP responses
- **Java web container**
  - Platform or engine that provides a runtime environment for Java-based web applications
  - Ex: Apache Tomcat, BEA WebLogic, JBoss
### **Common Components**

- **Third-party or open-source components that are often used alongside custom-built code**
  1. Authentication — JAAS, ACEGI
  1. Presentation layer — SiteMesh, Tapestry
  1. Database object relational mapping — Hibernate
  1. Logging — Log4J
### ASP.NET

- **Microsoft's web application framework**
  - **Competitor to Java platform**
- **Uses .NET Framework, which provides a virtual machine (the Common Language Runtime) and a set of powerful APIs (Application Program Interfaces)**
- **Applications can be written in any .NET language, such as C# or VB.NET**
### **Visual Studio**

- **Powerful development environment for ASP.NET applications**
- **Easy for developers to make a web application, even with limited programming skills**
- **ASP.NET helps protect against some common vulnerabilities, such as cross-site scripting, without requiring any effort from the developer**
### PHP

- Originally "Personal Home Page", now "PHP Hypertext Processor"
- Often used on LAMP servers
  - Linux, Apache, MySQL, and PHP
- Free and easy to use, but many security problems
- Both in PHP itself and in custom code using it
**Common PHP Applications**

- Bulletin boards — PHPBB, PHP-Nuke
- Administrative front ends — PHPMyAdmin
- Web mail — SquirrelMail, IlohaMail
- Photo galleries — Gallery
- Shopping carts — osCommerce, ECW-Shop
- Wikis — MediaWiki, WakkaWikki
### Ruby on Rails

- **Allows rapid development of applications**
- **Can autogenerate much of the code if developer follows the Rails coding style and naming conventions**
- **Has vulnerabilities like PHP**
### SQL (Structured Query Language)

- **Used to access data in relational databases, such as Oracle, MS-SQL, and MySQL**
- **Data stored in tables, each containing rows and columns**
- **SQL queries are used to read, add, update, or delete data**
- **SQL injection vulnerabilities are very severe**
### XML (eXtensible Markup Language)

- **A specification to encode data in machine- readable form**
- **Markup uses tags**
```javascript
<pet>ginger</pet>
<pets><dog>spot</dog><cat>paws</cat></pets>
```

Tags may include attributes, which are name/value pairs:

```javascript
<data version="2.1"><pets>...</pets></data>
```

### Web Services and SOAP (Simple Object Access Protocol)

- **SOAP uses HTTP and XML to exchange data**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a5a11991-0a3b-4bba-9983-9e171807b5a4/image24.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46663G6P2PA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204528Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDlzcibBqvSTjXHUxVpJ6fRlYwCxo4FMH1jGe0I%2F1RnUAIgcOSiQL2d8MjB1202OUTMVHmMO%2FkwU4Oc1URNE04U4F8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDK70rxXKmDQjpuu0jSrcA%2BTwMeCIYMaF8Kg%2FdcTjrghoOvLyFzgGFNej9p55bbMon335EpYNavJlUlrqOP3NJ3NEqZHUP7YNY2dJ4f7UFV0ubXTOLOKg8KK75fSgV7YlgpSgkqOYy0za7LT8c%2FMNpBKR5LfNTU5F0VGcoX3xrTb732S6foxVK4d0ScdALar33D0yJKIyeKiGJqxGFMSMEcH08cHZWQR5fMC7Htxscz4gDMIvQ3zkESoiDwPGS3zHheUyEf1V%2BrPzaWQXWOUfC%2B0dwP9ydtfeJnenvwIlTQw6Uh%2FMUQAeFK4BwqpoRxdWdsnMPHKZTE7WGMcxZzdlzT3npvXFr9myFeKIImVn7DhQILSRVW7vZeOVioH3%2Fnn2RrFVSuiKYQoU3g5Z1utOjhsO881%2Bdp4uudZp5XKcgfS9UgD8oOnX0%2FFD3UsDJag1KUmp0mpUjsXVebM2q7KUfnsEunaKfBZHs0HEb7cxZjXcpz3FLqq3vYau4vjhKQwf94Ceg7fq8dUmWd0FhDX%2BDVyl%2BXg8weSByFU6C3zgJ6tnZHawKr9BpbDLtaxfJ9TxNULFmRvH2Ith%2FhrPMEGDhP4AWfLvk83GK%2BU%2FNjUjxbLhhT2jjD5hY7RZqieReh5hPZl0Dq1WMqS82uvYMLDHotQGOqUBs3QufEcV4ADMnZ008l6IPbZ0tUZqZzA854UhpQcLG4tr4UdxH8G6kTQzPqlVfDOPLqqo9zBUSeA6ToqdRlM7DYQzKnUkq%2BDWbQ7AJk8VFkqbBrKppK76DKqdp86XbsKoeOKImaUpuqjpqmwga2mmIQ%2BqEQchks7jSsaGtBsXPCsz1Xt1LWI0iIeQFQGrOO%2FTy8ZEDEz4n%2BTRWUFjb6M33yhYnYsn&X-Amz-Signature=1f9844283b8ab1b6b37643dd15758355adc43679489e268dda431012446b08e6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **If user-supplied data is incorporated into SOAP requests, it can have code injection vulnerabilities**
- **Server usually publishes available services and parameters using Web Services Description Language (WSDL)**
- **soapUI and other tools can generate requests based on WSDL file**
## Client-Side Functionality (in browser)

### HTML Hypertext Markup Language

- **HTML used for formatting "markup"**
- **XHTML is based on XML and is stricter than old versions of HTML**
### Hyperlinks

- **Clickable text that go to URLs**
- **Clicking this link:**
```javascript
<a href="129S/129S_S22.shtml" target="_blank"> CNIT 129S: Securing Web Applications</a>
```

- **Makes this request**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1271266b-93a7-4f25-a844-1ce81c2f716a/image27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=e85dd1a56b01678ba19ddf56df257103c602f9218aa255ffc7bbe6424db28c38&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### HTML Forms

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/42f4d52c-382e-4819-9c56-592bbb228549/image28.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=00608cd06e99f36af9582d96d585bac375abc863974bc526172ab6f9527394c3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/42cdd1cd-a206-4f5e-bfce-b47dbe0451a5/image29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=a3e7695ef30ec8918d1fa3bb2cbd0a38978ba79b0739783dbe6df17658930ff3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**HTTP Request**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/af79dc02-5507-430e-8463-0ff9df88190e/image30.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=bd91fa3581ec64dbac2d476a65ca6a1fd041417e683f67ed61821f155c3b7b1c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### multipart/form-data

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/98918a79-8c13-4919-a799-5c04953eddee/image31.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=9a92e8d31dfdfc2850a902fb96b57804071228be19625b5f5c527d583816ba87&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d4050ea6-30a5-470d-a646-5c9c1c1be859/image32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=f6a4ed0c8e3ed0c89a3a93732ea567d85d5f73a223f039bc297b45347508204a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Browser generates random boundary text**
**HTTP Request**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b044719c-7963-4128-b5e6-71d4b6b8fb95/image33.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=2d5d425e916d70f410e6881492b2a43ac2b2d1cc268f311f1f0728218fc2c09f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### CSS Cascading Style Sheets

- **Specifies format of document elements**
- **Separates content from presentation**
- **Has vulnerabilities, and can be used for attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/704b6c84-6847-48a1-b8ec-0bd6348d0f0b/image34.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5T5E6NM%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204528Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEZgOS5yLFxTsj1rJLhDNGr2r1Vhp%2FZTi2zzFVe6cQ%2B4AiEAg07xsEAKiQ6in7YqYgd02BGKxqz2LZIwjWw0Y8%2B3IQQqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDCxs%2BOBqynjLCFNUoyrcA%2Bzr0eS22x8XQKexex19uGhrEgsM9Vz7uf5yqNwvPvw1QwesQUyVuwO3nK2MG0zpcPPBI9fEJrEqFTTtbiq1IlUVNsvJxAlHArqDVNM79kC3DAt8HrDde6D0bkki2q06P4npJDmt2ODlAMBNG7PI6vN%2FXuBDNXuhqvJxeyTvfosmB2yjnoADsNmmfieoL7%2BMsbFolVw6VrbdrZYOB%2BbjfAbStj%2FBZi4hxxBEtIC8Gx3cKrpJFZSgET%2FWVXHeeBkvwd8AOaz51gf3Atnc%2FNk4h5g%2FYvChVpresAYx%2BXq9gT7PX4aBOUVD5pBQgXfphzvdl0RRpvOA15vMEyYiqturxFRZBakjQTj5gGPH08zqrjPKY9veg1RyrH9fw%2FYlul0yOZyIpSC4xuc5781eo5zoiQE9WR%2FV7sSGrxDujiYLhe9lIR%2BZMXptAKUguAcLeJhehwJJifLX2FS17eHxWSUPjy96jtaNb%2B2UAd%2BOrTZnBcTJo%2BJiS0r6S5H3B5DUJwxoRCM0ewXSRvyz1amH%2BhG6K8v21sDgMTmHO%2BGHJEbgCa%2FKgjO5dUtUFCNSncoDg4CirtYx60eISsTb8XO0mEnp1cNQDRVdhImh8Ncj8yf8%2B2lc%2B9ZJ7TniOCh92Lp5MOHFotQGOqUBt%2FbVLu82UfT7nH8KkK8TCCBgKJstw1cKnjrOatcyK5wDUhNsDPE22wi4l%2BVLmPkBE8rrej2E8xcCqcvMDaUZHQ3fapiz9b4ePHy7vQzr9%2BvAb7h3EcR6TT0FbDq6asVnlKP%2FTtXzPHihsFqHbkONRY2D4pLoihDwR85n5CL0mCjTNAB1dAUuELNQzi%2FQzsOKj9jPST8I3H2jeVUU%2F2EEKp5ltsqG&X-Amz-Signature=25ff4c792b15e4b5041b2966dbd55b5c75aa78952cbeb5528246dd2701627a85&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Javascript

- **Scripts that run in the client's browser**
- **Used to validate user-entered data before submitting it to the server**
- **Dynamically modify UI in response to user action, such as in drop-down menus**
- **Using Document Object Model (DOM) to control the browser's behavior**
### VBScript

- **Microsoft's alternative to JavaScript**
  - **Only supported in Internet Explorer (now obsolete)**
- **Edge does not support VBScript**
### Document Object Model DOM

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/75866999-a500-4527-a326-6e245327762f/image35.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ST2GLAE4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCncZZDon1N5T6Hb94wjs7RzjaemyIRfm0J9J0%2FHN1SbgIgSJ15tSYwaUOAwPyFp2I7R6nfESvigB4eQUmrRldkJK4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNNB5jEt%2F4ZDirTUtCrcA0wpDQlWqeZej0z%2FK66Hq9UPPanIxsqhDlOCxgq1Iu%2BAj%2BzZ8qjAykaQ3tuNrlLMr8LKStTrlyXWLPMpKk7pcQwcSM6Xdl%2B2B3hq2aQ625M%2BpqqZ9p%2By28IML58BNwnI5wCfwczLBFRmRIvKM8Z%2BlyO%2FAexp4NpPfvoGOKBeefYXmUzH4tXwb61wpPnA%2BOgGrCuqZr%2F7a%2B2USTPE5YKE8YrreWtYo635aP4Kkpz2Wful%2FfCUI2H7qQINChlqPaO3OG5isPMUWncKvGSdqJ2uKOjD1ykflrlAdOVG1lOcs5DJAJo8pQ16vB7vmm1NN0abdYhhF3xHDfveilmnjnpL2lJRytTSqzcjB92MOYgyf6LpgI8%2FjzbUw2xKn5nzzJDBFMd1xuOAsUd0bLys9uwXFaeGa6G%2FebSYxIWJIHvxZimMTpr4L8yrSzg5WuDjGs0Gb9HwUiH9DjyBgisnq23bwkohRJOXzlUi2a9PSulWzOU8r7c5snseUcmTAb7bAZq%2F9%2FOUh6atjQUg7LeLkv68MrVq9Tz3%2FJtk7UdIo4lsObDuhpGnEMh%2BL65%2FYQtn%2B%2Bu9V8QNvwILFWkA4Zk2jpdDJT0ZyjJqVCiaTMNyExyqIzWT9YNZW5Y7b3KV8b7uMO%2FFotQGOqUB6khuHPkNPxAU0%2BA4QDj1a6t%2BSRg9SupXYJGGBAbaDszI9onuO%2BDb2czebc94wOYnS4%2BPLf1phVZXCRr5LnSyH2TJK7gdfVOzK92vBsGMU0igUQvh2NluE4wU%2FCsPk0R1VNcZNhOnUBfUMtKoeq5ssjnYN%2B%2BhrAEDb2azJduDausxTIquflf%2BCehA3XLOAPNsGBFeKeJ2kgypv60w66Opv76iF0aI&X-Amz-Signature=dba3eda011fd86bf44042e33f31b4041b21b7816532fd57c249a099e1ae69a19&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> Using the DOM

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2ec15e97-1724-42f5-ae5d-78a178e002b7/image36.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WKUE2FOZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204530Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAFXwnR5TEktUw%2FVZVSabNv8lbJrSQo0in%2FlzshurZ%2BfAiAaM02vPQ3LSK0tkBGJGiku0zoqnkrixzl85drrMvHQtyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMwnGoC0yv%2FllCPLRlKtwDYKq6LbBesBsp%2B5XPhl3ICiI3Fcr%2FBbxLGj9GDhVLTT5%2Bu9Aupj3FL5UxdZdkG0uSKz1235x9XIOIEFVTY8MEUsjMKHd7XbmHcxU5AguYNHJ0mLTkfw9qFGMUENt%2F2YPr3siw7UDAL0HjVEq4lEJwB5es8nJopVAYi86Yr%2BMdLPZLqj9C0xPZajOIPr6q8v8kkVpePkY%2Fv%2FNqPc2dT%2FKvKNcPa6VFr3qFiQYvdVACo8ayau%2BoxOtb64Eu09j8mz%2Bz35xYWWvO3Vt2K%2FnafQskmw5FtJx3sLA0CLpbJQpYBJ4QX3LCKy8ukzuP%2BRPotpJpYzXgTJTofW4HP5Y1vC7giLIwv84OZA%2F%2FCFikjGQ3nteMLqYIUJ8mX4u5RId6MwWlvAaWdAQZbet0wKUpQx9GWaHc2zbWIiWcfCxwSacl9SSIv5IfA5Sp9JT76wi3QbKOxmLVCDyF%2B0VhyER6YcxNQYt4LDs7JJgk8zcbwsyhmdMEt9x1dYNdm3DKM6fmj1hVBOHZ2nl8D7wPMhOnL3fpVxd2WA%2BuRaK8RZp2BD8pzU6mv58LgV4IZek4hnvnYBdsdT7G3eQ%2FBoPVxHywHfKNRWwFWZwqPJQH0SLE0ekPlggjmUstaxgik30KMN0wssai1AY6pgH4%2FHZnLSYYVg7t8K1%2F7%2BbvhfdapeYQVLNL66MIWIimg6NeZKhJ%2BR9mhyo9SAeMRPaUOSjGL2JJulS7f4jlY%2F9WIBpf4%2BXr38P1s1henBJwTss2AJBqK4VwT%2BUnKGyqkWEmgIffSwZhhAwS3YmDjUFLdYgQwnubXSAM%2FwvKKK3M%2FZXRsekjtUbQR%2FjkIvnRFki7Vu9nVx9RPuEk1Yw3MognTrg9zYF%2F&X-Amz-Signature=b6a94aa56dbb6b3925d1053b9944110af6041a7635d74ca4c8d73ae5252e6d7e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dbc01141-0948-4d3a-afea-92ce6da91c23/image37.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WJ6DMHRN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204530Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDbAhmc4Oz7oaS2HTjnbtfpJakcyAvOqSp8ClwPvlTlSAiBP%2Finu3Gn5%2FP2rkMPBboMb1rlIeBVDY593LVO4mo11OiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMmLdo2WGfG7e0aKXeKtwDhKQOb4h%2FgCH79so1FXy7N%2B0xRsip4r2HXL5wgiEgVh0uUW3Lvq%2F0eCIEeZHuwz9ZOBPxhadawh0xWVw8PRXMAxA2iF%2FdYYTfveb7F%2BXCAH2eWP4Hvp2hrc3FotwduVDXQq5kl2Zy5e7CgETaQkvy%2FzSIgXqMQKlKTcJokpjDxUmFCsJuNboGClxGBLf1dh4rQRi535u8DTCvhRhwd8Sadckp6cNMdjRPHoLkbaB9caz4AM6tBZaFxJOIiNzhDj5yxtImw5vhXCHvzgmNx%2FAyfjQaCZQX74LBGxRhc6kYPc%2FAuwiHCLPZo65%2BETEilNGMqg6BDfe4fADOETGudLDOkiys6Y9uJDBWOHVqUfQwWFcnxQGXl6ibtOa1yBiK4ZyHXNVyfnJNpjd0k3FvjJTmMoUNS2DEJtkqOErHlSAVg35W1bNfRrOTyVbmaM5F7ZAj%2BXeMS%2BVwS26Q%2Blb1440u1CPhplCU8eMCrk9uzhvQod1txiZUv5Z5dN8HPfT%2BHokzLIdloF5IFXVaxhpQP%2FlLTWIUlL4KYbjgGTOBevBt9TCcp1RNCA27fM65y0d9Zj42qc1yeUFDXGqTamcE%2Fb5xelCioeMcTZCn%2FCm33aageOTDYjMu1xCMGlFDy2ww6cii1AY6pgGwLwEqC4oVrEOOxcyg31WFbgegQ6GTDSPnnI1KTARwGrzR7tLVyNq%2FZHwBIFbH0C5KtUWUtdv%2B5VuHPcxNJqOwhS0Joxfdtm3n%2FKXTogf6%2BBtE7Dhl30VLyNJLfsGwqGSmCnSbzRlIoB2e9MlQI5FwM08uXEqWKje2ucLNf9NJdk0H6BkaPfynokH5jb5KgDSV0HYRW5lBXLKI64A4AN77U156tNTZ&X-Amz-Signature=5c856e4e8f265b78e66a8f100fae2c72f4c13bb109b624141d6a0843998023e2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


### Ajax Asynchronous JavaScript and XML

- **Client-side scripts can fetch data without reloading the entire page**
- **Allow you to drag Google Maps around**
Example

- **Google Maps API**
- **Links Ch 3h, 3i**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/78714397-b67f-409f-a927-863918602b6a/image39.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=e5253f19258be8274ecfd43a383f14247f08f66190810cd85edb703ca47fd886&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### JSON JavaScript Object Notation

- **Client-side JavaScript uses the XMLHttpRequest API to request data from a server**
- **Data is returned in JSON format:**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d5107810-cf7f-4c9f-b8b6-2c8a27972b11/image40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=8def52235c40fdf88a076dbc56a9a4357780e4a6b12cbc4a04801846b7a6b4e3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Updating Data with JSON**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8a052a4a-a1ca-4118-befa-dcdbdd60673f/image41.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=daf966450faa4ca423e7badc99d8073e16064127649a936d15d937a607fddc8d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Same-Origin Policy

- **Prevents content from different origins interfering with each other in a browser**
- **Content from one website can only read and modify data from the same website**
  - **Ex: scripts on Facebook can't read or write to data on your online banking page**
- **When this process fails, you get Cross-Site Scripting, Cross-Site Request Forgery, and other attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e5b710f9-ba71-4b37-aefa-2910a24531f7/image42.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=44b3ad17dac6d60586cd4638311fdec55a582140f49f780424dfc5fe59dcdd06&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### HTML5

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/23f86878-d345-432c-9655-70265b205510/image43.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=51703b4d40a5f3091cd706a39a3cf2170372408ef3da954ccd5478580fb2a1d2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Web 2.0

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb698da1-5c1c-4c62-a4b6-c51ba2dcc468/image44.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=1e3f4e85e4d7768c1847144399927a25ce6547769eca1a6f5ae8c88070c72af7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Browser Extensions

- Java applets
ActiveX controls
Flash objects
Silverlight objects
- **Many security problems**
- **More and more restricted in modern browsers**
## State and Sessions

- **Stateful data required to supplement stateless HTTP**
- **This data is held in a server-side structure called a *****session***
- **The session contains data such as items added to a shopping cart**
- **Some state data is stored on the client, often HTTP cookies or hidden form fields**
# Encoding Schemes

## URL Encoding

- **URLs may contain only printable ASCII characters**
  - **0x20 to 0x7e, inclusive**
- **To transfer other characters, or problematic ASCII characters, over HTTP, they must be URL- encoded**
%3d — =
n %25 — %
n %20 — Space
n %0a — New line
n %00 — Null byte

A further encoding to be aware of is the + character, which represents a
URL-encoded space (in addition to the %20 representation of a space).

**Note**

For the purpose of attacking web applications, you should URL-encode any of the following characters when you insert them *as data* into an HTTP request:

space%? & =; + #

## Unicode Encoding

- **Supports all the world's writing systems**
- **16 bits per character, starting with %u**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47b64dda-ccec-466f-acab-9e4d27e4ab45/image46.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=cc56bfa96308452bc0f3515285e2ec0131cdf3c048bd2e7f5556ce3d2b01a9c9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## UTF-8 Encoding

- **Variable length**
- **Uses % character before each byte**
- **Unicode and UTF-8 are often used to bypass filters in attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cb7a482a-10d9-4991-bce0-9b465e154b3a/image47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=109a730794e65168f6f2345ff990867b2ad7db535c3988b6a22e1d5b636e6110&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## HTML Encoding

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49134948-39a5-47ff-bb0f-f2a6a005ff6d/image48.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=3c859df66c4b6966315606c233e6e33d334f389082ccd0ff48f7ffcbdbefb984&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **HTML-encoding user data before sending it to another user is used to prevent Cross-Site Scripting attacks**
## Base64 Encoding

- **Represents binary data using 64 ASCII characters**
  - **Six bits at a time**
- **Used to encode email attachments so they can be sent via SMTP**
- **Uses this character set**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ff2ff46-574e-4c04-90bd-efe1270e15d4/image50.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=c0d84dbef13a1cba38b3ecaf165bc64dfef40d57bcf6b13801c86d7584137b99&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## Hex Encoding

- **Hexadecimal numbers corresponding to each ASCII character**
- **ABC encodes to 414243**
> Remoting and Serialization

Frameworks

- **Allows client-side code to use server-side APIs as if they were local**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/71a6c101-20cd-4b8c-af4b-816924af918c/image51.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46654CSD6J6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1DTcAZ8j3lEFmvAlZr41vU5GlvsLjx46RcW4W%2BwHGNQIhAKl7HZelQPx9rkGOVouH1lk2PB0speiOrYFfCQf79GsMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwZT32%2BsiRwZTrFElcq3APQXI8KGZjT9DGjet6IffgSkMNtsVZ2YhJfSlG8F%2FtoVhQNv3sZsv%2F40XUMmZy40jTXwKfcoDRGOY3tTAETmAAnwdjojjvvGuyOB2aWK8c04xWXRECqw1eiQ3imRi%2F%2BC%2BOX6DWCtXojQ%2FSMZCnObxNCXQOc0nyrp5fVI5CKok%2FZeSKkmafg70zRSJsNuTMcrqH3482RQv%2FouObwUylSIUi7TxmvEhQ3FqFhdX0NFtl60A1%2Fk0uFy5%2BTKATlW9j3FH5T0wRUEhtaGyzTKxJxAGXRdH4lQAxlAaCtlJOFdxxBkH1qXDNYtEe2JFmqiv3gzzQJOiCr9UGN37rQFVjyKG4tXKX%2BQNzyKJjhTFacno8nvUbOak7sb17Hg3GO3KpHp32u5qpVoTXA4P4iIn5AQuA2y7ZtIHbKbLh5BEsbYjLjSFlrMhUZF9DJFvpd9N957D7sScOCpjThFYMV21AESfJ6Wh0e015RjyKtQQYczGldGuYSFQtX03oJZLVEIojzgsS0i0sP6nzhKmGv9P6DoUVyfbNiZ2fJ1Rw3V2dDZMSs5y%2BuJ2bp6BYRt5qKmkbNDkjwudvY3CNHyp6MmjnWU7mImT4XAZoBrgWKkREKW8jNEOq5INXNY4Hwkmm6EzCRxqLUBjqkARryb0N0p1Ex11TBfciTDsn%2Buxqxm6C6UpivCVu%2B1F0Z585RAhAczkVDSyRDe7kVhZCzo9z%2FhVKZOTH1wV%2BgRNQ68ppiV7bIxCiyQbVJjGM9SlXH1e1AQNkPaxZ69EGOPOCO4UnaQ75w04y7swVuHFaLZH%2BrsIXsyubp%2F2V9BKpq9lDCBGnOWeYXf6SmsFSMQ31%2FO0QrLwcQfAoWKFIm6shE4S8z&X-Amz-Signature=fc8a630120431553f9fc0e37fc482a14b74be23e9087ed4d1b28bc307aefc978&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

