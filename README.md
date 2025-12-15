import React, { useState, memo } from 'react';

const PostItem = memo(({ post, currentUser, onLike, onRepost, onCommentClick, onViewProfile, onEdit, onDelete }) => (
  <div className="bg-gray-900 rounded-xl p-4 mb-4 border border-gray-700">
    <div className="flex items-center mb-3">
      <div className="w-10 h-10 bg-blue-500 rounded-full mr-3"></div>
      <div>
        <div 
          className="font-bold text-blue-400 hover:text-blue-300 cursor-pointer flex items-center"
          onClick={() => onViewProfile(post.authorId)}
        >
          {post.username}
          {post.isDeveloper && (
            <span className="ml-1 text-blue-400">✓</span>
          )}
        </div>
        <div 
          className="text-gray-400 text-sm hover:text-gray-300 cursor-pointer"
          onClick={() => onViewProfile(post.authorId)}
        >
          {post.handle}
        </div>
      </div>
      <div className="ml-auto text-gray-400 text-sm">{post.time}</div>
    </div>
    <div className="mb-4">{post.content}</div>
    <div className="flex justify-between items-center pt-4 border-t border-gray-700">
      <div className="flex space-x-6">
        <button 
          className="flex items-center text-gray-400 hover:text-white"
          onClick={() => onCommentClick(post.id)}
        >
          💬 <span className="ml-1">{post.comments}</span>
        </button>
        <button 
          className={`flex items-center ${post.repostedBy.includes(currentUser?.id) ? 'text-green-400' : 'text-gray-400 hover:text-white'}`}
          onClick={() => onRepost(post.id)}
        >
          🔄 <span className="ml-1">{post.reposts}</span>
        </button>
        <button 
          className={`flex items-center ${post.likedBy.includes(currentUser?.id) ? 'text-pink-500' : 'text-gray-400 hover:text-white'}`}
          onClick={() => onLike(post.id)}
        >
          {post.likedBy.includes(currentUser?.id) ? '❤️' : '♡'} <span className="ml-1">{post.likes}</span>
        </button>
      </div>
      
      {currentUser && post.authorId === currentUser.id && (
        <div className="flex space-x-2">
          <button 
            onClick={() => onEdit(post)}
            className="text-gray-400 hover:text-blue-400 text-sm"
          >
            Edit
          </button>
          <button 
            onClick={() => onDelete(post.id)}
            className="text-gray-400 hover:text-red-400 text-sm"
          >
            Hapus
          </button>
        </div>
      )}
    </div>
  </div>
));

const CommentItem = memo(({ comment, onViewProfile }) => (
  <div className="bg-gray-800 rounded-lg p-3">
    <div 
      className="font-bold text-blue-400 hover:text-blue-300 cursor-pointer text-sm flex items-center"
      onClick={() => onViewProfile(comment.authorId)}
    >
      {comment.author}
      {comment.isDeveloper && (
        <span className="ml-1 text-blue-400">✓</span>
      )}
    </div>
    <div 
      className="text-gray-400 hover:text-gray-300 cursor-pointer text-sm"
      onClick={() => onViewProfile(comment.authorId)}
    >
      {comment.authorHandle}
    </div>
    <div className="text-gray-300 text-sm mt-1">{comment.content}</div>
    <div className="text-gray-500 text-xs mt-2">{comment.time}</div>
  </div>
));

export default function App() {
  const [currentScreen, setCurrentScreen] = useState('auth');
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [isGuest, setIsGuest] = useState(false);
  const [authMode, setAuthMode] = useState('login');
  
  // Akun developer BinnApps: 0 following, 1 juta followers
  const allUsers = [
    { 
      id: 'dev1', 
      name: 'BinnApps Developer', 
      username: 'binndev', 
      password: 'binnprst1123',
      bio: 'Official Developer - BinnApps Platform', 
      followers: 1000000,
      following: 0,
      posts: 0,
      banned: false,
      isDeveloper: true,
      verified: true,
      followedBy: [],
      followingList: []
    },
    { 
      id: '1', 
      name: 'Ahmad Rizki', 
      username: 'ahmadrizki45', 
      password: 'password123',
      bio: 'AI Enthusiast & Developer', 
      followers: 1250, 
      following: 842, 
      posts: 0,
      banned: false,
      isDeveloper: false,
      verified: false,
      followedBy: [],
      followingList: []
    },
    { 
      id: '2', 
      name: 'Sarah Wijaya', 
      username: 'sarahwijaya78', 
      password: 'sarahpass',
      bio: 'Travel Blogger & Photographer', 
      followers: 2340, 
      following: 567, 
      posts: 0,
      banned: false,
      isDeveloper: false,
      verified: false,
      followedBy: [],
      followingList: []
    },
  ];

  const [posts, setPosts] = useState([
    {
      id: '1',
      authorId: '1',
      username: 'Ahmad Rizki',
      handle: '@ahmadrizki45',
      content: 'Baru saja menyelesaikan proyek AI yang sangat menarik! Gabungan antara machine learning dan computer vision untuk deteksi dini penyakit tanaman. Siapa yang tertarik kolaborasi?',
      media: null,
      likes: 156,
      likedBy: ['dev1'],
      comments: 2,
      commentList: [
        {
          id: 'c1',
          authorId: 'dev1',
          author: 'BinnApps Developer',
          authorHandle: '@binndev',
          content: 'Keren banget! Ini bisa jadi game changer di bidang pertanian. Mau kolaborasi?',
          time: '1 jam yang lalu',
          isDeveloper: true
        },
        {
          id: 'c2',
          authorId: '2',
          author: 'Sarah Wijaya',
          authorHandle: '@sarahwijaya78',
          content: 'Wah keren! Boleh juga dong diajari cara buatnya?',
          time: '45 menit yang lalu',
          isDeveloper: false
        }
      ],
      reposts: 1,
      repostedBy: ['dev1'],
      time: '2 jam yang lalu',
      isDeveloper: false
    },
    {
      id: '2',
      authorId: '2',
      username: 'Sarah Wijaya',
      handle: '@sarahwijaya78',
      content: 'Hari ini cuaca sempurna untuk jalan-jalan ke taman kota! 🌸 Siapa yang mau ikut weekend ini? #WeekendVibes #Jakarta',
      media: { type: 'image', url: 'placeholder-image' },
      likes: 89,
      likedBy: [],
      comments: 1,
      commentList: [
        {
          id: 'c3',
          authorId: '1',
          author: 'Ahmad Rizki',
          authorHandle: '@ahmadrizki45',
          content: 'Asik! Boleh ikut juga?',
          time: '30 menit yang lalu',
          isDeveloper: false
        }
      ],
      reposts: 0,
      repostedBy: [],
      time: '4 jam yang lalu',
      isDeveloper: false
    },
  ]);

  const [authData, setAuthData] = useState({
    loginEmail: '',
    loginPassword: '',
    registerName: '',
    registerEmail: '',
    registerPassword: '',
    registerConfirmPassword: ''
  });

  const [currentUser, setCurrentUser] = useState(null);
  const [viewedProfile, setViewedProfile] = useState(null);
  const [showComments, setShowComments] = useState(null);
  const [newComment, setNewComment] = useState('');
  const [showPostModal, setShowPostModal] = useState(false);
  const [postContent, setPostContent] = useState('');

  // Real-time interaction functions
  const handleLike = (postId) => {
    if (isGuest || !currentUser || currentUser.banned) {
      alert('Silakan login untuk menyukai postingan');
      return;
    }
    
    setPosts(prevPosts => 
      prevPosts.map(post => {
        if (post.id === postId) {
          const alreadyLiked = post.likedBy.includes(currentUser.id);
          if (alreadyLiked) {
            return {
              ...post,
              likes: post.likes - 1,
              likedBy: post.likedBy.filter(id => id !== currentUser.id)
            };
          } else {
            return {
              ...post,
              likes: post.likes + 1,
              likedBy: [...post.likedBy, currentUser.id]
            };
          }
        }
        return post;
      })
    );
  };

  const handleRepost = (postId) => {
    if (isGuest || !currentUser || currentUser.banned) {
      alert('Silakan login untuk repost postingan');
      return;
    }
    
    setPosts(prevPosts => 
      prevPosts.map(post => {
        if (post.id === postId) {
          const alreadyReposted = post.repostedBy.includes(currentUser.id);
          if (alreadyReposted) {
            return {
              ...post,
              reposts: post.reposts - 1,
              repostedBy: post.repostedBy.filter(id => id !== currentUser.id)
            };
          } else {
            return {
              ...post,
              reposts: post.reposts + 1,
              repostedBy: [...post.repostedBy, currentUser.id]
            };
          }
        }
        return post;
      })
    );
  };

  const handleAddComment = (postId) => {
    if (isGuest || !currentUser || currentUser.banned) {
      alert('Silakan login untuk berkomentar');
      return;
    }
    
    if (newComment.trim() === '') {
      alert('Komentar tidak boleh kosong');
      return;
    }
    
    const comment = {
      id: `c${Date.now()}`,
      authorId: currentUser.id,
      author: currentUser.name,
      authorHandle: `@${currentUser.username}`,
      content: newComment.trim(),
      time: 'Baru saja',
      isDeveloper: currentUser.isDeveloper || false
    };
    
    setPosts(prevPosts => 
      prevPosts.map(post => {
        if (post.id === postId) {
          return {
            ...post,
            comments: post.comments + 1,
            commentList: [...post.commentList, comment]
          };
        }
        return post;
      })
    );
    setNewComment('');
  };

  const toggleComments = (postId) => {
    setShowComments(showComments === postId ? null : postId);
  };

  const handleLogin = () => {
    if (authData.loginEmail && authData.loginPassword) {
      const email = authData.loginEmail.toLowerCase();
      const password = authData.loginPassword;
      
      if (email === 'binndev@gmail.com' && password === 'binnprst1123') {
        const devUser = allUsers[0];
        setCurrentUser(devUser);
        setIsLoggedIn(true);
        setIsGuest(false);
        setCurrentScreen('home');
        return;
      }
      
      const userName = email.split('@')[0];
      const user = allUsers.find(u => u.username === userName);
      
      if (!user) {
        alert('Akun tidak ditemukan');
        return;
      }
      
      if (user.banned) {
        alert('Akun Anda telah dibanned');
        return;
      }
      
      if (user.password !== password) {
        alert('Password salah!');
        return;
      }
      
      setCurrentUser(user);
      setIsLoggedIn(true);
      setIsGuest(false);
      setCurrentScreen('home');
    }
  };

  const handleRegister = () => {
    const { registerName, registerEmail, registerPassword, registerConfirmPassword } = authData;
    
    if (!registerName || !registerEmail || !registerPassword) {
      alert('Semua field harus diisi');
      return;
    }
    
    if (registerPassword.length < 6) {
      alert('Password minimal 6 karakter');
      return;
    }
    
    if (registerPassword !== registerConfirmPassword) {
      alert('Password tidak cocok');
      return;
    }
    
    if (!registerEmail.includes('@')) {
      alert('Email tidak valid');
      return;
    }
    
    const baseUsername = registerName.toLowerCase().replace(/\s+/g, '');
    const randomNumbers = Math.floor(10 + Math.random() * 90);
    const generatedUsername = `${baseUsername}${randomNumbers}`;
    
    const newUser = {
      id: `user${Date.now()}`,
      name: registerName,
      username: generatedUsername,
      password: registerPassword,
      bio: 'Pengguna BinnApps',
      followers: 0,
      following: 0,
      posts: 0,
      banned: false,
      isDeveloper: false,
      verified: false,
      followedBy: [],
      followingList: []
    };
    
    setCurrentUser(newUser);
    setIsLoggedIn(true);
    setIsGuest(false);
    setCurrentScreen('home');
    alert(`Berhasil! Username Anda: @${generatedUsername}`);
  };

  const handleGuestMode = () => {
    setIsLoggedIn(true);
    setIsGuest(true);
    setCurrentScreen('home');
  };

  const handleLogout = () => {
    setIsLoggedIn(false);
    setIsGuest(false);
    setCurrentUser(null);
    setViewedProfile(null);
    setCurrentScreen('auth');
    setAuthData({
      loginEmail: '',
      loginPassword: '',
      registerName: '',
      registerEmail: '',
      registerPassword: '',
      registerConfirmPassword: ''
    });
  };

  // CREATE POST - Bisa dilakukan oleh semua akun yang login
  const handleCreatePost = () => {
    if (isGuest || !currentUser || currentUser.banned) {
      alert('Silakan login untuk membuat postingan');
      return;
    }
    
    if (postContent.trim() === '') {
      alert('Postingan tidak boleh kosong');
      return;
    }
    
    const newPost = {
      id: `post${Date.now()}`,
      authorId: currentUser.id,
      username: currentUser.name,
      handle: `@${currentUser.username}`,
      content: postContent.trim(),
      media: null,
      likes: 0,
      likedBy: [],
      comments: 0,
      commentList: [],
      reposts: 0,
      repostedBy: [],
      time: 'Baru saja',
      isDeveloper: currentUser.isDeveloper || false
    };
    
    setPosts(prevPosts => [newPost, ...prevPosts]);
    setPostContent('');
    setShowPostModal(false);
    
    // Update user post count
    const updatedUser = { ...currentUser, posts: (currentUser.posts || 0) + 1 };
    setCurrentUser(updatedUser);
    
    // Update allUsers array
    const updatedAllUsers = allUsers.map(u => 
      u.id === currentUser.id ? updatedUser : u
    );
  };

  const handleEditPost = (post) => {
    setPostContent(post.content);
    setShowPostModal(true);
  };

  const handleDeletePost = (postId) => {
    if (!currentUser || currentUser.banned) return;
    
    if (!window.confirm('Hapus postingan ini?')) return;
    
    setPosts(prevPosts => prevPosts.filter(post => post.id !== postId));
    
    const updatedUser = { ...currentUser, posts: Math.max(0, (currentUser.posts || 0) - 1) };
    setCurrentUser(updatedUser);
  };

  const viewUserProfile = (user) => {
    const foundUser = allUsers.find(u => u.id === user);
    if (foundUser) {
      setViewedProfile(foundUser);
      setCurrentScreen('profile');
    }
  };

  const viewUserFromPost = (userId) => {
    viewUserProfile(userId);
  };

  if (!isLoggedIn && currentScreen === 'auth') {
    return (
      <div className="min-h-screen bg-black flex items-center justify-center p-4">
        <div className="text-center max-w-md w-full">
          <div className="text-4xl font-bold text-blue-400 mb-2">BinnApps</div>
          <div className="text-gray-400 mb-8">Semua cara berinteraksi, dalam satu tempat.</div>
          
          {authMode === 'login' ? (
            <div className="space-y-3">
              <input type="email" placeholder="Email" value={authData.loginEmail} onChange={(e) => setAuthData(prev => ({ ...prev, loginEmail: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <input type="password" placeholder="Password" value={authData.loginPassword} onChange={(e) => setAuthData(prev => ({ ...prev, loginPassword: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <button onClick={handleLogin} className="w-full bg-blue-600 text-white py-3 rounded-full font-bold">Masuk</button>
              <button onClick={() => setAuthMode('register')} className="w-full text-blue-400 py-3 font-bold">Belum punya akun? Daftar</button>
              <button onClick={handleGuestMode} className="w-full text-gray-500 py-3 font-bold">Lanjut tanpa akun</button>
            </div>
          ) : (
            <div className="space-y-3">
              <input type="text" placeholder="Nama Lengkap" value={authData.registerName} onChange={(e) => setAuthData(prev => ({ ...prev, registerName: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <input type="email" placeholder="Email" value={authData.registerEmail} onChange={(e) => setAuthData(prev => ({ ...prev, registerEmail: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <input type="password" placeholder="Password" value={authData.registerPassword} onChange={(e) => setAuthData(prev => ({ ...prev, registerPassword: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <input type="password" placeholder="Konfirmasi Password" value={authData.registerConfirmPassword} onChange={(e) => setAuthData(prev => ({ ...prev, registerConfirmPassword: e.target.value }))} className="w-full bg-gray-800 text-white rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-blue-500" />
              <button onClick={handleRegister} className="w-full bg-blue-600 text-white py-3 rounded-full font-bold">Daftar</button>
              <button onClick={() => setAuthMode('login')} className="w-full text-blue-400 py-3 font-bold">Sudah punya akun? Masuk</button>
            </div>
          )}
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-black text-white">
      <div className="pb-20 p-4 max-w-2xl mx-auto">
        {currentScreen === 'home' && (
          <div>
            <div className="flex justify-between items-center mb-4">
              <h1 className="text-xl font-bold">Beranda</h1>
              <button onClick={() => setCurrentScreen('notifications')} className="text-xl">🔔</button>
            </div>
            {posts.map(post => (
              <PostItem 
                key={post.id}
                post={post}
                currentUser={currentUser}
                onLike={handleLike}
                onRepost={handleRepost}
                onCommentClick={toggleComments}
                onViewProfile={viewUserFromPost}
                onEdit={handleEditPost}
                onDelete={handleDeletePost}
              />
            ))}
          </div>
        )}
        
        {currentScreen === 'profile' && (
          <div className="p-4">
            <div className="bg-gray-800 rounded-xl p-6 mb-6">
              <div className="flex items-center mb-4">
                <div className="w-16 h-16 bg-blue-500 rounded-full mr-4"></div>
                <div className="flex-1">
                  <div className="flex items-center">
                    <h2 className="text-xl font-bold text-white">{(viewedProfile || currentUser)?.name}</h2>
                    {(viewedProfile || currentUser)?.verified && (
                      <span className="ml-2 text-blue-400">✓</span>
                    )}
                  </div>
                  <p className="text-blue-400">@{(viewedProfile || currentUser)?.username}</p>
                  <p className="text-gray-300 mt-2">{(viewedProfile || currentUser)?.bio}</p>
                </div>
              </div>
              
              <div className="flex justify-around py-4 border-t border-gray-700">
                <div className="text-center">
                  <div className="text-white font-bold">{(viewedProfile || currentUser)?.posts || 0}</div>
                  <div className="text-gray-400 text-sm">Posting</div>
                </div>
                <div className="text-center">
                  <div className="text-white font-bold">{(viewedProfile || currentUser)?.following}</div>
                  <div className="text-gray-400 text-sm">Mengikuti</div>
                </div>
                <div className="text-center">
                  <div className="text-white font-bold">{(viewedProfile || currentUser)?.followers.toLocaleString('id-ID')}</div>
                  <div className="text-gray-400 text-sm">Pengikut</div>
                </div>
              </div>
            </div>
            
            <button 
              onClick={handleLogout}
              className="w-full bg-pink-600 text-white py-3 rounded-lg font-bold"
            >
              Logout
            </button>
          </div>
        )}
        
        {currentScreen === 'notifications' && (
          <div className="text-center py-12">
            <div className="text-4xl mb-4">🔔</div>
            <p className="text-gray-500">Belum ada notifikasi</p>
          </div>
        )}
        
        {currentScreen === 'chat' && (
          <div className="text-center py-12">
            <div className="text-4xl mb-4">📭</div>
            <p className="text-gray-500">Belum ada percakapan</p>
          </div>
        )}
      </div>

      {!isGuest && currentScreen === 'home' && (
        <button 
          onClick={() => setShowPostModal(true)}
          className="fixed bottom-20 right-4 w-10 h-10 bg-blue-600 rounded-full flex items-center justify-center text-lg text-white"
        >
          +
        </button>
      )}

      <div className="fixed bottom-0 left-0 right-0 bg-gray-900 border-t border-gray-700 flex justify-around py-2">
        <button onClick={() => setCurrentScreen('home')} className={`flex flex-col items-center text-xs ${currentScreen === 'home' ? 'text-blue-400' : 'text-gray-400'}`}>
          <div className="text-lg">🏠</div>
          <div>Beranda</div>
        </button>
        <button onClick={() => setCurrentScreen('search')} className={`flex flex-col items-center text-xs ${currentScreen === 'search' ? 'text-blue-400' : 'text-gray-400'}`}>
          <div className="text-lg">🔍</div>
          <div>Cari</div>
        </button>
        {!isGuest && (
          <button onClick={() => setShowPostModal(true)} className="flex flex-col items-center text-xs text-gray-400">
            <div className="text-lg">➕</div>
            <div>Post</div>
          </button>
        )}
        <button onClick={() => setCurrentScreen('chat')} className={`flex flex-col items-center text-xs ${currentScreen === 'chat' ? 'text-blue-400' : 'text-gray-400'}`}>
          <div className="text-lg">💬</div>
          <div>Chat</div>
        </button>
        <button onClick={() => { setViewedProfile(null); setCurrentScreen('profile'); }} className={`flex flex-col items-center text-xs ${currentScreen === 'profile' ? 'text-blue-400' : 'text-gray-400'}`}>
          <div className="text-lg">👤</div>
          <div>Profil</div>
        </button>
      </div>

      {/* Post Modal */}
      {showPostModal && !isGuest && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-end">
          <div className="bg-gray-800 w-full p-4 rounded-t-2xl">
            <div className="flex justify-between items-center mb-3">
              <h2 className="text-lg font-bold">Buat Postingan</h2>
              <button onClick={() => setShowPostModal(false)} className="text-xl text-gray-400">✕</button>
            </div>
            <textarea
              value={postContent}
              onChange={(e) => setPostContent(e.target.value)}
              placeholder="Apa yang sedang terjadi?"
              className="w-full bg-gray-700 text-white rounded-lg p-3 h-24 resize-none focus:outline-none focus:ring-1 focus:ring-blue-500 text-sm"
            />
            <div className="flex justify-between mt-3">
              <button 
                onClick={() => setShowPostModal(false)}
                className="px-4 py-1.5 text-gray-300 text-sm"
              >
                Batal
              </button>
              <button 
                onClick={handleCreatePost}
                className="px-4 py-1.5 bg-blue-600 text-white rounded font-bold text-sm"
              >
                Posting
              </button>
            </div>
          </div>
        </div>
      )}

      {/* Comments Modal */}
      {showComments !== null && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-end">
          <div className="bg-gray-800 w-full p-4 rounded-t-2xl max-h-96 overflow-y-auto">
            <div className="flex justify-between items-center mb-3">
              <h2 className="text-lg font-bold">Komentar</h2>
              <button onClick={() => setShowComments(null)} className="text-xl text-gray-400">✕</button>
            </div>
            
            <div className="flex mb-3">
              <input
                type="text"
                placeholder="Tulis komentar..."
                value={newComment}
                onChange={(e) => setNewComment(e.target.value)}
                className="flex-1 bg-gray-700 text-white rounded-full px-4 py-2 text-sm focus:outline-none focus:ring-1 focus:ring-blue-500"
                onKeyPress={(e) => e.key === 'Enter' && handleAddComment(showComments)}
              />
              <button 
                onClick={() => handleAddComment(showComments)}
                className="ml-2 bg-blue-600 text-white px-4 py-2 rounded-full text-sm"
              >
                Kirim
              </button>
            </div>
            
            {posts.find(p => p.id === showComments)?.commentList.map(comment => (
              <CommentItem 
                key={comment.id}
                comment={comment}
                onViewProfile={viewUserFromPost}
              />
            ))}
          </div>
        </div>
      )}
    </div>
  );
}
