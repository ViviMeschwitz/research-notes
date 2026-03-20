ステップ2に進め。setView で検索して、画面がどこで切り替わるか全部見つけろ。何箇所あるか、それぞれ何のアクションで切り替わるかを報告しろ。

## 解答 & 疑問
- 数 -> 9箇所
- 1  ->  const [view, setView] = useState<View>("list");
先ほどのuseStateによるview変数の定義に使われている。view変数が画面の現在位置を表すものだから、画面の切り替えを受け持つsetViewが使われているの？そもそも、setViewとは何？

- 2 ->const handleOpenBook = useCallback(async (bookId: string) => {
    await fetchBookDetail(bookId);
    setView("book-editor");
  }, [fetchBookDetail]);
1での定義によって、setView("book-editor");が機能するの？「本」タブで本をクリックが、本を開く操作に対応し、この操作でこの関数が呼び出されて、book-editor画面に切り替わる？

- 3 -> const handleBackFromBook = useCallback(async () => {
    setCurrentBook(null);
    setView("list");
    await fetchBooks();
  }, [fetchBooks]);
book-editor画面からlist画面に戻るボタンを押すことで、view変数の値がbook-editorからlistに変わる

- 4 -> const handleNewProject = () => {
    setCurrent(null);
    setView("session");
  };
新しいテクストボタンを押すと、current変数の値をnullにして、setViewによって、view変数の値をsessionにして、session画面に切り替える。

- 5 -> const handleOpenProject = async (id: string) => {
    const proj = await getProject(id);
    if (proj) {
      setCurrent(proj);
      setView("session");
      fetchVersions(id);
    }
  };
一覧のプロジェクトをクリックすると、そのテクスト自体がcurrent変数にsetされ、setViewによって、画面がsessionに変わる。

- 6 -> const handleBackToList = async () => {
    setView("list");
    setCurrent(null);
    setVersions([]);
    setBranchParentId(null);
    const [latest, latestBooks] = await Promise.all([
      loadProjects(),
      fetch("/api/books").then((r) => r.ok ? r.json() : []),
    ]);
    setProjects(latest);
    setBooks(latestBooks);
  };
画面をsessionからlistに戻す。

- 7 -> <button
            onClick={() => setView("irokawa")}
            className="flex-1 px-4 py-2.5 text-sm font-serif font-bold transition-colors bg-amber-50 text-amber-700 hover:bg-amber-100"
          >
            色河
          </button>
色河ボタンを押すとview変数の値がirokawaに変わる。

- 8 -> onBack={() => {
          setView("list");
          Promise.all([
            loadProjects(),
            fetch("/api/books").then((r) => r.ok ? r.json() : []),
          ]).then(([p, b]) => {
            setProjects(p);
            setBooks(b);
          });
        }}
View変数の値をirokawaからlistに変更

- 9 -> onNewText={() => {
          setCurrent(null);
          setView("session");
        }}
新しいテキストボタンを押すと、viewの値がirokawaからsessionに変わる。