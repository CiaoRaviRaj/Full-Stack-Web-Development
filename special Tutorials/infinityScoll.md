* Infinite scroll
    * app
        * import useBookSearch
            const [query, setQuery] = useState('');
            const [pageNumber, setPageNumber] = useState(1);
            const { books , hasMore, loading, error} = useBookSearch(query , pageNumber)
            const observer = useRef()
            const lastBookElementRef = useCallback( node => {
                if(loading) return
                if(observe.current) observer.current.disconnect()
                observer.current = new IntersectionObserver( enteries => {
                    if(entries[0].isIntersecting && hasMore) {
                        setPageNumber(prevPageNumber => prevPageNumber + 1) 
                    }
                })
                if (node) observe.current.observe(node)
            },[loading , hasMore])
            function handleSearch(e) {
                setQuery(e.target.value);
            }
        * return 
            * <>
                <input type="text" /> </input>
                <div>Title</div>
                <div>Title</title>
                {books.map((book, index) => {
                    if(books.length === index + 1) {
                        return <div ref={lastBookElementRef} key={book}>{book}</div>
                    }
                    return <div key={book}>{book}</div>
                })}
                ...
                <div>Loading....</div>
                </div>
    * useBookSearch(query, pageNumber)
        setLoading(true)
        setError(false)
        let cencel 
        * const [loading, setLoading] = useState(true)
        * const [error , setError] = useState(false);
        * const [books ,setBooks] = useState([]);
        * const [hasMore , setHasMore] =useState(false)
        * useEffect(() => {
            setBooks([])
        }, [query])
        * useEffect(() => {
            axios({
                method: "GET",
                url: "https://openlibrary.org/search.json"
                params: { q: query , page: pageNumber}
                cancel: new.axios.CancelToken(c => cancel = c)
            }).then(res => {
                res.data
                return [...new Set [...prevBooks, ...res.data.docs.map(b => b.title)]]
                setHasMore(res.data.docs.length > 0)
                setLoading(false)
            }).catch(e => {
                if (axios.isCancel(e)) return
                setError(true)
            })

        }, [query, pageNumber])

        return {
            loading, error , books, hasMore
        }
             