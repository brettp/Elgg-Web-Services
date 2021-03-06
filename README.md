Elgg Web Services
=================

List of Web Services
--------------------

### Core

 * site.test - Heartbeat method to test whether web services are up

	```
	$info = $client->get('site.test');
	var_dump($info);
	```

	```
	string 'Hello' (length=5)
	```

 * site.get_info - Get basic information about this Elgg site

	```
	$info = $client->get('site.getinfo');
	var_dump($info);
	```

	```
	object(stdClass)[135]
		public 'url' => string 'http://elgg-master.mbp/Users/brett/Devel/elgg/master' (length=52)
		public 'sitename' => string 'New Elgg site' (length=13)
		public 'language' => string 'en' (length=2)
	```


### User

 * user.get_profile_fields          Get profile fields
 
	```
	$info = $client->get('user.get_profile_fields');
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public 'description' => 
		object(stdClass)[13]
		  public 'label' => string 'About me' (length=8)
		  public 'type' => string 'longtext' (length=8)
	  public 'briefdescription' => 
		object(stdClass)[12]
		  public 'label' => string 'Brief description' (length=17)
		  public 'type' => string 'text' (length=4)
	  public 'location' => 
		object(stdClass)[11]
		  public 'label' => string 'Location' (length=8)
		  public 'type' => string 'location' (length=8)
	  public 'interests' => 
		object(stdClass)[10]
		  public 'label' => string 'Interests' (length=9)
		  public 'type' => string 'tags' (length=4)
	  public 'skills' => 
		object(stdClass)[9]
		  public 'label' => string 'Skills' (length=6)
		  public 'type' => string 'tags' (length=4)
	  public 'contactemail' => 
		object(stdClass)[8]
		  public 'label' => string 'Contact email' (length=13)
		  public 'type' => string 'email' (length=5)
	  public 'phone' => 
		object(stdClass)[7]
		  public 'label' => string 'Telephone' (length=9)
		  public 'type' => string 'text' (length=4)
	  public 'mobile' => 
		object(stdClass)[6]
		  public 'label' => string 'Mobile phone' (length=12)
		  public 'type' => string 'text' (length=4)
	  public 'website' => 
		object(stdClass)[5]
		  public 'label' => string 'Website' (length=7)
		  public 'type' => string 'url' (length=3)
	  public 'twitter' => 
		object(stdClass)[4]
		  public 'label' => string 'Twitter username' (length=16)
		  public 'type' => string 'text' (length=4)
	```
	
 * user.get_profile                 Get profile information

	```
	$params = array("username" => "admin");
	$info = $client->get('user.get_profile', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public 'description' => null
	  public 'briefdescription' => null
	  public 'location' => null
	  public 'interests' => null
	  public 'skills' => null
	  public 'contactemail' => null
	  public 'phone' => null
	  public 'mobile' => null
	  public 'website' => null
	  public 'twitter' => null
	```
	
 * user.save_profile              Update profile information
 
	```
	$profile = array('description' => 'description test',
					'briefdescription' => 'briefdescription test',
					'location' => 'India',
					'interests' => 'my interest',
					'skills' => 'my skills',
					'contactemail' => 'myemail@email.com',
					'phone' => '01234567890',
					'mobile' => '11234567890',
					'website' => 'http://mywebsite.com',
					'twitter' => 'tweet',
					);
	$params = array('username' => $this->user->username,
					'profile' => $profile
					);	
	$info = $client->post('user.save_profile', $params);
	var_dump($info);
	```
	
	```
	string 'Success' (length=7)
	```
	
 * user.get_user_by_email           Get all users registered with an email ID
 
	```
	$params = array('email' => 'tachyon.saket@gmail.com');
	$info = $client->get('user.get_user_by_email', $params);
	var_dump($info);
	```
	
	```
	array
		0 => string 'Admin' (length=5)
	```
	
 * user.check_username_availability Check availability of username

	```
	$params = array('username' => 'admin');	
	$info = $this->client->get('user.check_username_availability', $params);
	var_dump($info);
	```
	
	```
	boolean false
	```
	
 * user.register                    Register user
 
	```
	$params = array('name' => 'test',
					'email' => 'test2@test.org',
					'username' => 'test2',
					'password' => 'password',
					);	
	$info = $this->client->get('user.register', $params);
	var_dump($info);
	```
	
	```
	int 8654
	```
	
 * user.friend.add                  Add a user as a friend
 
	```
	$params = array('username' => array ('type' => 'string'),
					'friend' => array ('type' => 'string'),
					);	
	$info = $this->client->get('user.friend.add', $params);
	var_dump($info);
	```
	
	```
	boolean true
	```
	
 * user.friend.remove               Remove a user from friend
 
	```
	$params = array('username' => array ('type' => 'string'),
					'friend' => array ('type' => 'string'),
					);	
	$info = $this->client->get('user.friend.remove', $params);
	var_dump($info);
	```
	
	```
	boolean true
	```
	
 * user.friend.get_friends          Get friends of a user
 
	```
	$params = array('username' => 'admin',
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('user.friend.get_friends', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
		public 'tachyon' => string 'Saket Saurabh' (length=13)
	```
	
 * user.friend.get_friends_of       Obtains the people who have made a given user a friend
 
	```
	$params = array('username' => 'tachyon',
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('user.friend.get_friends', $params);
	var_dump($info);
	```

	```
	object(stdClass)[3]
		public 'Admin' => string 'Administrator' (length=13)
	```
	
### Blog

 * blog.save_post         Make a blog post
 
	```
	$params = array('username' => 'admin',
					'title' => 'Test blog post',
					'text' => 'text of blog post',
					),
	$info = $this->client->get('blog.save_post', $params);
	var_dump($info);
	```
	
	```
	boolean true 
	```
	
 * blog.get_post          Read a blog post
 
	```
	$params = array('guid' => 53,
					'username' => 'admin'
					),
	$info = $this->client->get('blog.get_post', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public 'title' => string 'This is a new blog' (length=18)
	  public 'content' => string 'this is the content of the latest blog' (length=38)
	  public 'excerpt' => string '' (length=0)
	  public 'tags' => string 'blog' (length=4)
	  public 'owner_guid' => string '43' (length=2)
	  public 'access_id' => string '2' (length=1)
	  public 'status' => string 'published' (length=9)
	  public 'comments_on' => string 'On' (length=2)
	```
	
 * blog.delete_post       Delete a blog post
 
	```
	$params = array('guid' => 53,
					'username' => 'admin'
					);
	$info = $this->client->get('blog.delete_post', $params);
	var_dump($info);
	```
	
	```
	string 'Blog post deleted.' (length=18)
	```
	
 * blog.get_friends_posts  Get latest blog post by friends
 
	```
	$params = array('username' => 'admin',
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('blog.get_friends_posts', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '55' => 
		object(stdClass)[4]
		  public 'time_created' => string '1310124191' (length=10)
		  public 'title' => string 'This is a new blog' (length=18)
		  public 'content' => string 'this is the content of the latest blog' (length=38)
		  public 'excerpt' => string '' (length=0)
		  public 'tags' => string 'blog' (length=4)
		  public 'owner_guid' => string '43' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'status' => string 'published' (length=9)
		  public 'comments_on' => string 'On' (length=2)
	```
	
 * blog.get_latest_posts Latest blog post by a user or by all user
 
	```
	$params = array('username' => 'admin',
						'limit' => 1,
						'offset' => 0,
					);
	$info = $this->client->get('blog.get_latest_posts', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '49' => 
		object(stdClass)[4]
		  public 'time_created' => string '1310027828' (length=10)
		  public 'title' => string 'title' (length=5)
		  public 'content' => string 'text' (length=4)
		  public 'excerpt' => string 'excerpt' (length=7)
		  public 'tags' => string 'tags' (length=4)
		  public 'owner_guid' => string '36' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'status' => string 'published' (length=9)
		  public 'comments_on' => string 'On' (length=2)
	```
 
### Group

 * group.join                  Joining a group
	
	```
	$params = array('username' => 'tachyon',
					'groupid' => 72,
					);
	$info = $this->client->get('group.join', $params);
	var_dump($info);
	```
	
	```
	string 'Successfully joined group!' (length=26)  
	```
	
 * group.leave                 Leaving a group
 
	```
	$params = array('username' => 'tachyon',
					'groupid' => 72,
					);
	$info = $this->client->get('group.leave', $params);
	var_dump($info);
	```
	
	```
	string 'Successfully left group' (length=23)
	```
	
 * group.forum.save_post       Posting a new topic to a group
 
	```
	$params = array('username' => 'admin',
						'groupid' => 71,
						'title' => 'testing post',
						'desc' => 'hello i am testing web services',
					);
	$info = $this->client->get('group.forum.save_post', $params);
	var_dump($info);
	```
	
	```
	string 'The discussion topic was created.' (length=33)
	```
	
 * group.forum.delete_post     Deleting a topic from a group
 
	```
	$params = array('username' => 'admin',
					'topicid' => 84,
					);
	$info = $this->client->get('group.forum.delete_post', $params);
	var_dump($info);
	```
	
	```
	string 'Discussion topic has been deleted.' (length=34)
	```
	
 * group.forum.get_latest_post Get latest post in a group
 
	```
	$params = array('groupid' => 47,
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('group.forum.get_latest_post', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '56' => 
		object(stdClass)[4]
		  public 'title' => string 'test' (length=4)
		  public 'description' => string '<p>test</p>' (length=11)
		  public 'owner_guid' => string '36' (length=2)
		  public 'container_guid' => string '47' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'time_created' => string '1310144929' (length=10)
		  public 'time_updated' => string '1310144929' (length=10)
		  public 'last_action' => string '1310321462' (length=10)
	```
	
 * group.forum.get_replies     Get replies on a post
 
	```
	$params = array('postid' => 56,
					  'limit' => 1,
					  'offset' => 0,
					);
	$info = $this->client->get('group.forum.get_replies', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '2' => 
		object(stdClass)[4]
		  public 'value' => string '<p>this i smy reply</p>' (length=23)
		  public 'name' => string 'group_topic_post' (length=16)
		  public 'enabled' => string 'yes' (length=3)
		  public 'owner_guid' => string '36' (length=2)
		  public 'entity_guid' => string '56' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'time_created' => string '1310310194' (length=10)
		  public 'name_id' => string '71' (length=2)
		  public 'value_id' => string '70' (length=2)
		  public 'value_type' => string 'text' (length=4)
	```
	
 * group.forum.save_replies    Post a reply
  
	```
	$params = array('username' => 'admin',
						'postid' => 56,
						'text' => 'My reply',
					);
	$info = $this->client->post('group.forum.save_replies', $params);
	var_dump($info);
	```
	
	```
	boolean true
	```
	
 * group.forum.delete_reply    Delete a reply
 
	```
	$params = array('username' => 'admin',
					'id' => 6,
					);
	$info = $this->client->post('group.forum.delete_reply', $params);
	var_dump($info);
	```
	
	```
	string 'Discussion reply has been deleted.' (length=34)
	```

### Wire

 * wire.save_post        Making a wire post
 
	```
	$params = array('username' => 'admin',
					'text' => 'test wire post',
					);
	$info = $this->client->post('wire.save_post', $params);
	var_dump($info);
	```
	
	```
	boolean true
	```
	
 * wire.get_post         Read latest wire post of user
 
	```
	$params = array('username' => 'admin',
					);
	$info = $this->client->get('wire.get_post', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public 'guid' => string '64' (length=2)
	  public 'time_created' => string '1310558739' (length=10)
	  public 'description' => string 'wire post' (length=9)
	```
	
 * wire.get_friends_posts Read latest wire post by friends
 
	```
	$params = array('username' => 'admin',
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('wire.get_friends_posts', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '64' => 
		object(stdClass)[4]
		  public 'time_created' => string '1310558739' (length=10)
		  public 'description' => string 'wire post' (length=9)
	```
	
 * wire.delete_posts Read latest wire post by friends
 
	```
	$params = array('username' => 'admin',
					'wireid' => 64,
					);
	$info = $this->client->get('wire.delete_posts', $params);
	var_dump($info);
	```
	
	```
	string 'The wire post was successfully deleted.' (length=39)
	```
 
### File

 * file.get_files    Get file list by all users or a pecific user

	```
	$params = array('limit' => 1,
					  'offset' => 0,
					);
	$info = $this->client->get('wire.get_files', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '58' => 
		object(stdClass)[4]
		  public 'title' => string 'deploy' (length=6)
		  public 'owner_guid' => string '43' (length=2)
		  public 'container_guid' => string '43' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'time_created' => string '1310301409' (length=10)
		  public 'time_updated' => string '1310301409' (length=10)
		  public 'last_action' => string '1310301409' (length=10)
	```
	
 * file.get_files_by_friend Get file list by friends
 
	```
	$params = array('username' => 'admin',
					'limit' => 1,
					'offset' => 0,
					);
	$info = $this->client->get('wire.get_files_by_friend', $params);
	var_dump($info);
	```
	
	```
	object(stdClass)[3]
	  public '58' => 
		object(stdClass)[4]
		  public 'title' => string 'deploy' (length=6)
		  public 'owner_guid' => string '43' (length=2)
		  public 'container_guid' => string '43' (length=2)
		  public 'access_id' => string '2' (length=1)
		  public 'time_created' => string '1310301409' (length=10)
		  public 'time_updated' => string '1310301409' (length=10)
		  public 'last_action' => string '1310301409' (length=10)
	```
 
### Likes

 * likes.add Like an entity
 
	```
	$params = array('entity_guid' => 64),
					);
	$info = $this->client->post('likes.add', $params);
	var_dump($info);
	```
	
	```
	string 'You now like this item' (length=22)
	```
	
 * likes.delete Unlike an entity
 
	```
	$params = array('entity_guid' => 64),
					);
	$info = $this->client->post('likes.add', $params);
	var_dump($info);
	```
	
	```
	string 'Your like has been removed' (length=26)
	```
	
 * likes.count Number of likes to an entity
 
	```
	$params = array('entity_guid' => 64),
					);
	$info = $this->client->get('likes.add', $params);
	var_dump($info);
	```
	
	```
	int 3
	```