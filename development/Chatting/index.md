---
layout: post
title: "React로 채팅 구현 시 로직에 대해"
subtitle: "#채팅 #React #messaging #socket"
type: "개발 로직"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: ""
order: 10
date: 2023-04-30
comments: true
---

최근에 메시지 시스템 개발할 일이 많았는데, 아래의 기본 로직을 바탕으로 구현했다.
각 채팅방을 채널로 구분하고, 최초 접속 시 해당 채널에 소캣 접속 후 메시지를 매핑한다.
스크롤로 가장 오래된 메시지에 접근하면, 더 이전의 메시지를 불러오는 형태다.
스크롤을 70%이상 올라갔을 때 메시지를 불러올 수도 있고, 이건 기획 의도대로 진행하면 된다.
그리고 채널 변경 시, 해당 소캣의 구독을 취소하고 새로운 채널로 접속하여 다시 메시지를 가져온다.
필요한 내용들을 메모용도로 적었다.

<br/>

```javascript
const getMessages = async (id: string) => {
  setLoading(true);
  const response = await getThingMessage(id, page);
  if (response.success) {
    const messages = response.data;
    // console.log("getMessages page:", page, "thing message:", messages);
    if (messages.length === 0) setLoading(false);

    // created_at 데이터가 DB에 추가된 시간
    // content.timestamp 데이터 실제 생성 시간

    let list: any = [];
    if (messages && messages.length > 0) {
      let a = new Set(messages.map((value: any) => moment(value.created_at).locale("ko").format(dateFormat)));
      let dates = Array.from(a);
      // console.log("지금까지 chatList:", chatList);
      if (chatList?.length === 0) {
        // 처음 매핑
        dates.map((date) => {
          let day: any = [];
          messages.map((value: any) => {
            if (date === moment(value.created_at).locale("ko").format(dateFormat)) {
              day.unshift(value);
            }
          });

          list.push({ date: date, chat: day });
        });
        console.log("list:", list);
        setChatList([...list.reverse()]);

        // 처음 메시지 가져오면 스크롤 맨 아래로
        if (container) {
          container?.current?.scrollTo({ top: container.current.scrollHeight });
        }
      } else {
        // 기존 메시지에 새로운 메시지 추가시
        list = chatList;
        messages.map((message: any) => {
          let index = list.findIndex((ele: any) => moment(message.created_at).locale("ko").format(dateFormat) === ele.date);
          // console.log('index:', index, message.created_at);
          index !== -1
            ? list[index].chat.unshift(message)
            : list.unshift({
                date: moment(message.created_at).locale("ko").format(dateFormat),
                chat: [message],
              });
        });

        console.log("list:", list);
        setChatList([...list]);
      }

      setLoading(false);
      setLoadedChat(true);
    }
  }
};
```

```javascript
const handleOnScrollStop = async (e: any) => {
  if (page && chatList?.length > 0 && container.current.scrollTop === 0) {
    setChatScrollHeight(container.current.scrollHeight);
    setPage({
      ...page,
      offset: page.offset + page.limit,
      last_created_at: chatList[0].chat[0].created_at,
    });
  }
};
```

```javascript
const sendMessage = (message: any) => {
  // console.log("message:", message);
  console.log("selectedThing.channel_id:", selectedThing.channel_id);

  io.emit(
    "message",
    JSON.stringify({
      command: "create", //  modify or delete
      message: {
        type: "thing",
        from: meId,
        to: selectedThing.channel_id, // channelId
        created_at: moment().locale("ko"),
        content: message,
      },
    })
  );
};
```

```javascript
function addMessage(response: any) {
  const today = moment().locale("ko").format(dateFormat);

  let copyArray = chatList;
  if (copyArray.length > 0) {
    const idx = copyArray.findIndex((value: any) => {
      return value.date === today;
    });

    if (idx !== -1 && copyArray[idx]) {
      copyArray[idx] = {
        ...copyArray[idx],
        chat: [...copyArray[idx].chat, response],
      };
    } else {
      copyArray = copyArray.concat({
        date: today,
        chat: [response],
      });
    }

    setChatList(copyArray);
    container?.current?.scrollTo({ top: container.current.scrollHeight, behavior: "smooth" });
  }
}

function onMessage(response: any) {
  try {
    // console.log("onMessage:", response);
    addMessage(response);
  } catch (e) {
    console.log("onMessage e:", e);
  }
}
```

```javascript
useEffect(() => {
  // 최초 메시지 매핑 후 채널 조인
  if (selectedThing?.channel_id && loadedChat) {
    console.log("join:", selectedThing?.channel_id);
    io.emit(
      "join",
      JSON.stringify({
        channel_id: selectedThing?.channel_id,
      })
    );

    console.log("채널 변경, 메시지 구독", selectedThing?.channel_id);
    io.on("message", onMessage);
    io.on("system", onSystem); // 개인간 메시지 외 시스템적으로 필요한 메시지 구독
  }
}, [loadedChat]);

useEffect(() => {
  if (chatList?.length === 0 && selectedThing?.id) {
    console.log("selectedThing:", selectedThing?.id);
    getMessages(selectedThing?.id);

    return () => {
      console.log("메시지 구독 취소", selectedThing?.channel_id);
      io.emit("leave", JSON.stringify({ channel_id: selectedThing.channel_id }));
      io.off("message", onMessage);
      io.off("system", onSystem);
    };
  }
}, [selectedThing?.id]);

useEffect(() => {
  if (chatList?.length > 0) {
    // 스크롤 위치 조정
    container?.current?.scrollTo({ top: container?.current.scrollHeight - chatScrollHeight });
  }
}, [chatList]);

useEffect(() => {
  if (page.offset !== 0) {
    getMessages(selectedThing?.id);
  }
}, [page.offset]);
```
