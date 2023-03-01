* # Chat app with react stream
    * stream a module with a chat facilities in very easier way
    * for Chat app Set up
        * server
            * npm init -y
            * npm i fastify
                * it is similar like express
            * cors set up
                * npm i @fastify/cors
            * server .js
                * import fastify from 'fastify'
                * import cors from "@fastify/cors"

                * const app = fastify()
                * app.register(cors, {origin: process.env.CLIENT_URL})
                * app.register(userRouters)
                * app.listen({port : parseInt(process.env.PORT!)})
                    * ! :- it can not be undefine
                    * npm i --save-dev @types/node
                * npm i --save-dev nodemon ts-node
                    * ts-node for type script in node
            
            * routes
                * import { FastifyInstance} from "fastify";
                * import {StreamChat} from "stream-chat"

                * const streamChat = StreamChat.getInstance(
                    process.env.STREAM_API_KET!,
                    process.env.STREAM_PRIVATE_API_KEY!
                )
                * const TOKEN_USER_ID_MAP = new Map<string, string>()
                * export async function userRoutes( app: FastifyInstance) {
                    * app.post<{ Body : { id: string ; name: string; image?: string }}>("/signup", 
                    * async(req, res) => {
                        const { id, name , image} = req.body
                        if(id == null || id === "" || name == null || name === "" ) {
                            return res.status(400).send()
                        }

                        // TODO : CHECK for existing users
                        const existingUsers = await streamChat.queryUsers({id})
                        if ( existingUsers.users.length > 0) {
                            return res.status(400).send("user ID taken")
                        }


                        // creating user
                        streamChat.upsertUser({ id, name, image})

                    })
                    * app.post<{ Body : { id: string ; name: string; image?: string }}>("/login", 
                    * async(req, res) => {
                        * const { id} = req.body
                        if(id == null || id === "" ) {
                            return res.status(400).send()
                        }

                        await  { users: [user]} = await streamChat.queryUsers({ id })
                        if (user = null) return res.status(401).send()
                        const token = streamChat.createToken(id)
                        * TOKEN_USER_ID_MAP.set(token, user.id)

                        return {
                            token,
                            user: {
                                name: user.name,
                                id: user.id,
                                image: user.image
                            }
                        }



                    })
                    * app.post<{Body: {token: string}}>("/logout", async(req, res) => {
                        const token = req.body.token
                        if( token == null || token === "" ) return res.status(400).send()

                        * const id = TOKEN_USER_TO_MAP.get(token)
                        if (id == null) return res.status(400).send()

                        await streamChat.revokeUserToken(id, newDate())
                        TOKEN_USER_ID_MAP.delete(token)
                    })
                }
            * stream set up 
                * sign up
                * chat messaging
                    * overview
                        * api
                * npm i stream-chat

        * client
            * npm create vite@latest
            * npm i react-router-dom
            * npm i -D tailwindcss postcss autoprefixer
                * npm tailwindcss init -p
                * copy and paste config and index.css file code to respected file from website
            * set up react query
                * npm i @tanstack/react-query axios
            * set up front end stream chat
                * npm i stream-chat stream-chat-react
            * set up router
                * main.tsx
                    * import { RouterRrovider }
                    const queryClient = new QueryClient()
                    * <QueryClientProvider client={queryClient}>
                        * <RouterRrovider router={router}/>
                    </QueryClientProvider>
                    
                * router.tsx
                    * import { createBrowserRouter } 
                    * export const router = createBrowserRouter([
                        {
                            element: <ContextWrapper />
                            children: [
                                {
                                    path: "/"
                                    element: <RootLayout />
                                    children: [
                                        { index: true , element: <Home />},
                                        {path: "/channel", children: [
                                            {path: "new", element: <h1>New CHannel</h1> }
                                        ]}
                                        
                                    ]
                                },

                                {
                                    element: <AuthLayout />
                                    children: [
                                        { path: 'login', element: <Login />},
                                        {path : 'signup' , element: <Signup />}
                                    ]
                                }
                            ]
                            
                        }
                    ])
                    * function ContextWrapper() {
                        return <AuthProvider>
                            <Outlet />
                        </AuthProvider>
                    }

            * pages
                * layouts
                    * AuthLayout.tsx
                        * export function AuthLayout() {
                            const location = useLocation()
                            const isLoginPage = location.pathname === "/login"

                            return <FullScreenCard> 
                                <FullScreenCard.Body>
                                    <Outlet />
                                </FullScreenCard.Body>
                                <FullScreenCard.BelowCard>
                                    <Link to={isLoginPage ? "/signup" : "/login"}>
                                        {
                                           isLoginPage ? "Create Accont" : "Login" 
                                        }
                                    </Link>
                                </FullScreenCard.BelowCard>
                            </FullScreenCard.Body>
                            
                            // Outlet for children render
                        }
                    * RootLayout.tsx
                        * export function RootLayout() {
                            const { user } = useAuth ()
                            if( user == null ) return <Navigate to="/login" />
                            return <Outlet />
                            
                            // Outlet for children render
                        }
                    
                * Login.tsx
                    * export function Login() {
                        const { login, user } = useAuth()
                        const usernameRef = useRef<HTMLInputElement>(null)
                        if (user != null ) return <Navigate to="/" />
                        function handleSubmit ( e: FormEvent) {
                            e.preventDefault()
                            if(login.isLoading) return 
                            const username = usernameRef.current?.value
                            
                            if ( username == null || username === ""){
                                return
                            }


                            login.mutate({
                                id: username,
                            })
                        }
                        * return (
                            * <>
                                * <h1 className="text-3xl font-bold mb-8 text-center"> Login </h1>
                                * <from onSubmit={handleSubmit} className="grid grid-cols-[auto, 1fr] gap-x-3 gap-y-5 items-center justify-items-end">
                                    <label htmlFor="username">Username</label>
                                    <Input id="username" required ref={usernameRef} />
                                    <Button 
                                    disabled={login.isLoading}
                                    className="col-span-full" type="submit" > Login</Button>
                                </form>
                            </h1>
                        )
                    }
                * Signup.tsx
                    * export function Signup() {
                        const { signup } = useAuth()
                        const usernameRef = useRef<HTMLInputElement>(null)
                        const nameRef = useRef<HTMLInputElement>(null)
                        const imageUrlRef = useRef<HTMLInputElement>(null)
                        function handleSubmit ( e: FormEvent) {
                            e.preventDefault()
                            if(signup.isLoading) return 
                            const username = usernameRef.current?.value
                            const name = nameRef.current?.value
                            const imageUrl = imageUrlRef.current?.value
                            if ( username == null || username === "" || name == null || name === ""){
                                return
                            }


                            signup.mutate({
                                id: username, name, image: imageUrl
                            })
                        }
                        * return (
                            * <>
                                * <h1 className="text-3xl font-bold mb-8 text-center"> Sign up </h1>
                                * <from onSubmit={handleSubmit} className="grid grid-cols-[auto, 1fr] gap-x-3 gap-y-5 items-center justify-items-end">
                                    <label htmlFor="username">Username</label>
                                    <Input id="username" pattern="\s*" required ref={usernameRef} />
                                     <label htmlFor="name">name</label>
                                    <Input id="name"  required ref={nameRef} />
                                     <label htmlFor="imageUrl">Image Url</label>
                                    <Input id="imageUrl" type="url" ref={imageUrlRef} />
                                    <Button 
                                    disabled={signup.isLoading}
                                    className="col-span-full" type="submit" > Sign Up</Button>
                                </form>
                            </h1>
                        )
                    }
                * Home.tsx  
                    * import "stream-chat-react/dist/css/index.css" in index.js
                    * export function Home () {
                        const { user , streamChat } = useLoggedAuth()
                        if ( streamChat == null) return <LoadingIndicator />

                        return (
                            <Chat client={streamChat}>
                                <ChannelList List={Channels} sendChannelsToList filter=[{members: { $in: [user.id]}}] />
                                <Channel>
                                    <Window>
                                        <ChannelHeader />
                                        <MessageList />
                                        <MessageInput />
                                    </Window>
                                </Channel>
                            </Chat>
                            )
                    }
                    * function Channels({ loadedChannels}: ChannelListMessengerProps) {
                        const navigate = useNavigate()
                        const { logout } = useLoggedInAuth()
                        const { setActiveChannel, channel: activeChannel } = useChatContext()
                        * return (
                            * <div className="w-60 flex-col gap-4 m-3 h-full">

                                * <Button onClick={navigate("/channel/new")}>New Conversation </Button>

                                * <hr className="border-gray-500" />

                                * {loadedChannels != null && loadedChannels.length > 0 ? loadedChannels.map(channel => {
                                    * const isActive = channel === activeChannel

                                    * const extraClasses = isActive ? "bg-blue-500 text-white" ? "hover: bg-blue-100 bg-gray-100"

                                    * return <button onClick ={() => setActiveChannel(channel)} disabled={isActive} className={`p-4 rounded-lg flex gap-3 item-center ${extraClasses}`} key={channel.id}>
                                        
                                        * {channel.data?.image && <img src={channel.data.image} className="w-10 h-10 rounded-full object-center /> }
                                        * <div className="text-ellipsis overflow-hidden whitespace-nowrap">
                                            {channel.data?.name || channel.id}
                                        </div>
                                    <button>
                                }) : "No Conversation"}

                                <hr className="border-gray-500 mt-auto">

                                * <Button onClick={() => logout.mutate()} disabled={logout.isLoading}>Logout</Button>
                            </div>
                        )
                    }
                * channel
                    * new.tsx
                        * export function NewChannel () {
                            const { streamChat , user} = useLoggedInAuth()
                            const createChannel = useMutation({
                                mutationFn: ({ name, memberIds, imageUrl}: {
                                    name: string,
                                    memberIds: string,
                                    imageUrl?.string
                                }) => {
                                    if(streamChat == null) throw Error("Not connected")
                                    return streamChat.channel("messaging" , crypto.randomUUID, {
                                        name,
                                        image: imageUrl,
                                        members: [user.id, ...memberIds]
                                    }).create()
                                }
                                onSuccess: () => navigate("/")
                            })
                            
                            * const nameRef = useRef<HTMLInputElement>(null)
                            * const imageUrlRef = useRef<HTMLInputElement>(null)
                            * const memberIdRef = useRef<SelectInstance<{label: string, value: string}>>(null)
                            * const users = useQuery({
                                queryKey: ["stream", "users"]
                                queryFn: () => streamChat!.queryUsers({
                                    id: { $ne: user.id },{
                                        name: 1
                                    }
                                }),
                                enabled: streamChat != null
                            })
                            * function handelSubmit(e : FormEvent) {
                                e.preventDefault()
                                const name = nameRef.current?.value
                                const imageUrl = imageUrlRef.current?.value
                                const selectOptions = memberIdsRef.current?.getValue()
                                if(name == null || name === "" || selectOptions == null || selectOptions.length === 0) {
                                    return 
                                }
                                createChannel.mutate({
                                    name, imageUrl, memberIds: selectOptions.map(option => option.value)
                                })
                            }
                            * return (
                                * <FullScreenCard>
                                    * <FullScreenCard.Body>
                                        * <h1 className="text-3xl font-bold mb-8 text-center"> New Channel </h1>
                                        * <from onSubmit={handleSubmit} className="grid grid-cols-[auto, 1fr] gap-x-3 gap-y-5 items-center justify-items-end">
                                            <label htmlFor="name">Username</label>
                                            <Input id="name" required ref={nameRef} />
                                            <label htmlFor="imageUrl">Username</label>
                                            <Input id="imageUrl" required ref={imageUrlRef} />
                                            <label htmlFor="members">Menbers</label>
                                            <Select ref={memberIdRef} id="members" required isMulti className={{container: () => "w-full}}
                                            isLoading={users.isLoading}
                                            option={users.data.users.map(user => {
                                                return: {
                                                    value: user.id, label: user.name || user.id
                                                }
                                            })}
                                            />
                                            
                                            <Button 
                                                disabled={createChannel.isLoading}
                                                className="col-span-full" type="submit" > Create Error
                                            </Button>
                                         </form>
                                    </FullScreenCard.Body>
                                    <FullScreenCard.BelowCard>
                                        <Link to="/">Back</Link>
                                    </FullScreenCard.BelowCard>
                                </<FullScreenCard>>
                                )
                        }
            * components
                * FullScreenCard.tdx
                    * contents for 
                        * type FullScreenCardProps = {
                            children: ReactNode
                        }
                    * export function FullScreenCard({ children }: FullScreenCardProps) {
                        return <div className= "flex justify-center items-center min-h-screen bg-gray-100>
                            <div className="max-w-md w-full> {children} </div>
                        </div>
                    }
                    * it is now create a wrapper that used to show the content in the screen 
                    * it has the type as FullScreenCardProps
                    * now make content specific function
                    * FullScreenCard.Body = function ({ children } : FullScreenCardProps) {
                        return <div className="shadow bg-white p-6 rounded-lg"> { children } </div>
                    }
                    * FullScreenCard.BelowCard = function ({ children } : FullScreenCardProps) {
                        return <div className="mt-2 justify-center flex gap-3"> { children } </div>
                    }
                    
                * export const Input = forwardRef<HTMLInputElement, DetailedHTMLProps<InputHTMLAttributes<HTMLInputElement>,<HTMLInputElement>>>(({children, className, ...rest}, ref) => {
                    * // set forwardRef type of HTMLInputElement
                    * // DetailedHTMLProps<InputHTMLAttributes<HTMLInputElement>,<HTMLInputElement>> these all code do same thing as like normal react aap doing to fetch props

                    * return <input className={`py-1 px-2 border-gray-400 focus:border-blue-500 outline-none rounded w-full ${className}`} {...rest} ref={ref}>
                })
                * export const Button = forwardRef<HTMLButtonElement, DetailedHTMLProps<ButtonHTMLAttributes<HTMLButtonElement>,<HTMLButtonElement>>>(({children, className , ...rest}, ref) => {
                    * // set forwardRef type of HTMLInputElement
                    * // DetailedHTMLProps<ButtonHTMLAttributes<HTMLButtonElement>,<HTMLButtonElement>> these all code do same thing as like normal react aap doing to fetch props

                    * return <button className={`border-2 border-gray-900 bg-blue-600 rounded p-2 w-full text-white fond-bold hover:bg-blue-500 focus:bg-blue-400 transition-colors disabled:bg-gray-500 ${className}`} {...rest} ref={ref}> {children} </button>
                })
                * Link.tsx
                    * import { LinkProps, Link as RouterLink}
                    * export function Link ({ children , className, ...rest}: LinkProps) {
                        return (
                            <RouterLink
                            {...rest}
                            className={`text-blue-500 underline underline-offset-2 ${classNme}`}
                            >

                            </ <RouterLink>>
                        )
                    }
            * context
                * AuthContext.tsx
                    * type AuthContext  = {
                        * signup: UseMutationResult<AxiosResponse, unknown , User>
                        * login: UseMutationResult< {token: string , user: User}, unknown , string>
                        * user?: User,
                        * streamChat?: StreamChat
                        * logout: UseMutationResult<AxiosResponse, unknown , void>
                    }
                    * const Context = createContext<AuthContext | null>(null)
                    * export function useAuth() {
                        return useContext(Context) as AuthContext
                    }

                    * export function useLoggedAuth() {
                        return useContext(Context) as AuthContext & Required<Pick<AuthContext, "user">>
                    }
                    * type AuthProviderProps = {
                        children: ReactNode
                    }
                    * export function AuthProvider ({children}: AuthProviderProps) {
                        const navigate = useNavigate()
                        const [user, setUser] = useState<User>()
                        const [token, setToken] = useState<string>()
                        const [streamChat, setStreamChat] = useState<StreamChat>()
                        * const signup = useMutation({
                            mutationFn: (user: User) => {
                                return axios.post(`${import.meta.env.VITE_SERVER_URL}/signup`, user)
                            }
                            onSuccess(data, variable, context) {
                                navigate("/login")
                            }
                        }) 
                        * const login = useMutation({
                            mutationFn: (id: string) => {
                                return axios.post(`${import.meta.env.VITE_SERVER_URL}/signup`, id)
                                .then(res => {
                                    return res.data as {token : string ; user: User}
                                })
                            }
                            onSuccess(data) {
                                setUser(data.user)
                                setToken(data.token)
                            }
                        })
                        * const logout = useMutation({
                            mutationFn: () => {
                                return axios.post(`${import.env.VITE_SERVER_URL}/logout`, { token })
                            }
                            onSuccess() {
                                setUser(undefined)
                                setToken(undefined)
                                setStreamChat(undefined)
                            }
                        })
                        * useEffect(() => {
                            * if(token == null || user == null) return 
                            const chat = new StreamChat(import.meta.env.VITE_PUBLIC_KEY)
                            * if(chat.tokenManager.token === token && chat.userID === user.id) return 
                            * let isInterrupted = false
                            * const connectPromise = chat.connectUser(user, token)
                            .then(() => {
                                if(isInterrupted) return 
                                setStreamChat(chat)
                            })
                            * return () => {
                                * isInterrupted = true
                                * setStreamChat(undefined)
                                * connectPromise.then(() => {
                                    chat.disconnectUser()
                                })
                            }
                        }, [token, user])
                        return <Context.Provider value={{ signup, login, user , streamChat , logout}}>
                        {children}
                        </Context.Provider >
                    }
            * 

