### [과제] 숙련주차 과제 답

숙련주차 과제
구글폼으로 더욱 상세히 적었습니다 ............... ㅜ

- 추가하기 버튼을 클릭해도 추가한 아이템이 화면에 표시되지 않음.
  디스패치 부분에 조작 X
  form에서 받은 정보들을 넘겨주지 않았음. 입력 후 내용 초기화만 시켜줬음
  그래서
  setTodo({
  id: todos.length + 1,
  title: todo.title,
  body: todo.body,
  isDone: false,
  });
  라는 코드를 추가하여 아래 form에서 받아온 정보들을 넣어줌.
  dispatch(addTodo(todo));

- 추가하기 버튼 클릭 후 기존에 존재하던 아이템들이 사라짐.
  디스패치의 case ADD_TODO 부분에 앞의 것들을 모두 없애고 새롭게 추가한 아이템만 넣어주었기 때문임
  스프레드 로 기존에 있던 아이템들 나열 후 새로운 아이템 추가. 다시묶어주기
  return {
  ...state,
  todos: [...state.todos,action.payload],
  };
  이렇게!
  이러한 문제가 발생한 이유는 store 의 todos 안에 todos의 형태로 아이템들? 정보들이 있었기 때문임
- 삭제 기능이 동작하지 않음.
  리듀서에 딜리트 케이스가 없었음.
  filter이용하여 state.todos에서 아이디값이 일치하지 않는 것을 제외해줌
  case DELETE_TODO:
  const newList = state.todos.filter((item)=>item.id!==action.payload)
  alert("삭제완료!")
  return {...state, todos: newList}

- 상세 페이지에 진입 하였을 때 데이터가 업데이트 되지 않음.
  일단 todos 라는 스토어의 todos라는 항목에 진입해야 하므로
  const todos = useSelector((state) => state.todos.todos);
  (한번 더 들어가줘야함.. state.todos 라고만 하면.. 뒤에있는 빈 todo까지 불러와줘서 정신 못체림.. 이름이 비슷해서 헷갈림.)
  params이용하여 / 뒤의 숫자 받아오기.
  todos 중에서 id값이 일치하는 것 찾아서
  그 찾은 아이템의 정보를 적어주면 됨 !

- 완료된 카드의 상세 페이지에 진입 하였을 때 올바른 데이터를 불러오지 못함.
  아이디값이 String()이용 하여 그냥 다 문자열로 비교하게 만들기
- 취소 버튼 클릭시 기능이 작동하지 않음.
  dipatch 에서 action creator 함수에 보내줄 정보값을 적어주지 않았음. 따라서 todo.id 라는 값을 payload로 보내주면 됨
- 과제를 마쳤다면 배포도 한번 해볼까요?
