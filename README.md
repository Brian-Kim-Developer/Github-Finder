# Github Finder
## Introduction
The aim of this project is to provide users with search engine service that enables them to reach out people who are using Github.
With this service, the clients will be able to simply access to summary of the targets' information - including Name, Location, Hireable Status, Professional Summary, Current Company, Website, Followers & Followoing, Public Repos & Public Gists, and Link to visit the Github Profile.

## Technologies
### React JS, React Hooks & Context

## APIs used for this project
https://api.github.com/users <br/><br/>
https://api.github.com/search/users?q=${text}&client_id=${process.env.REACT_APP_GITHUB_CLIENT_ID}&client_secret=${process.env.REACT_APP_GITHUB_CLIENT_SECRET} <br/><br/>
https://api.github.com/users/${username}?client_id=${process.env.REACT_APP_GITHUB_CLIENT_ID}&client_secret=${process.env.REACT_APP_GITHUB_CLIENT_SECRET} <br/><br/>
https://api.github.com/users/${username}/repos?per_page=5&sort=created:asc&client_id=${process.env.REACT_APP_GITHUB_CLIENT_ID}&client_secret=${process.env.REACT_APP_GITHUB_CLIENT_SECRET}

## Resources
#### Tips for Deploying NGINX (Official Image) with Docker
https://www.docker.com/blog/tips-for-deploying-nginx-official-image-with-docker/
#### Docs for the Github API:
https://developer.github.com/v3/
#### To Register Github App & Get Keys:
https://github.com/settings/applications/new

## References
#### How To Use Async Await in React (componentDidMount Async)
https://www.valentinog.com/blog/await-react/
#### What is preventDefault() in React?
https://www.robinwieruch.de/react-preventdefault
#### What is the meaning of {…this.props} in Reactjs
https://stackoverflow.com/questions/28452358/what-is-the-meaning-of-this-props-in-reactjs
