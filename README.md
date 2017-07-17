# Test
	public void setupClient(String configPath) throws IOException {
		String email;
		String userKey;
		String password;
		String scheme;
		String hostName;
		int port;
		String path;
		
		Properties config = new Properties();
		FileInputStream inputStream = null;
		try {
			inputStream = new FileInputStream(configPath);
		} catch (FileNotFoundException e) {
			throw new FileNotFoundException("Config file ("+ configPath + ") not found. " + 
					"Did you remember to make a copy from the template file?");
		}
		config.load(inputStream);
		email = config.getProperty("email");
		userKey = config.getProperty("user_key");
		password = config.getProperty("password");
		scheme = config.getProperty("scheme");
		hostName = config.getProperty("hostname");
		port = Integer.parseInt(config.getProperty("port"));
		path = config.getProperty("path");
		
		TrackviaClient client = TrackviaClient.create(path, scheme, hostName, 
				port, email, password, userKey);
		connector = new TrackViaConnector(client);
	}
