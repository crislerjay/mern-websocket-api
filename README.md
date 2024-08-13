API URL: https://mern-websocket-api.onrender.com/api/todos


for realtime update install socket.io-client on react

```
const [todos, setTodos] = useState([]);

  useEffect(() => {
    axios.get('http://localhost:3000/api/todos').then((response) => {
      console.log(response.data);
      setTodos(response.data);
    });

    socket.on('todoCreated', (todo) => {
      console.log('todoCreated');
      setTodos((prevTodos) => [...prevTodos, todo]);
    });

    socket.on('todoUpdated', (updatedTodo) => {
      console.log('todoUpdated');
      setTodos((prevTodos) =>
        prevTodos.map((todo) =>
          todo._id === updatedTodo._id ? updatedTodo : todo
        )
      );
    });

    socket.on('todoDeleted', (deletedTodo) => {
      console.log('todoDeleted');
      setTodos((prevTodos) =>
        prevTodos.filter((todo) => todo._id !== deletedTodo._id)
      );
    });

    return () => {
      socket.off('todoCreated');
      socket.off('todoUpdated');
      socket.off('todoDeleted');
    };
  }, []);
```
