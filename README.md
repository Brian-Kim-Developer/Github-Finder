# Github Finder
## Introduction
The aim of this project is to provide users with search engine service that enables them to reach out people who are using Github.
With this service, the clients will be able to simply access to summary of the targets' information - including Name, Location, Hireable Status, Professional Summary, Current Company, Website, Followers & Followoing, Public Repos & Public Gists, and Link to visit the Github Profile.

## Technologies
### React.js
### React Hooks & Context

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

## Production
#### 1. Modify GithubState.js
```
import React, { useReducer } from 'react';
import axios from 'axios';
import GithubContext from './githubContext';
import GithubReducer from './githubReducer';
import {
  SEARCH_USERS,
  SET_LOADING,
  CLEAR_USERS,
  GET_USER,
  GET_REPOS
} from '../types';

let githubClientId;
let githubClientSecret;

if (process.env.NODE_ENV !== 'production') {
  githubClientId = process.env.REACT_APP_GITHUB_CLIENT_ID;
  githubClientSecret = process.env.REACT_APP_GITHUB_CLIENT_SECRET;
} else {
  githubClientId = process.env.GITHUB_CLIENT_ID;
  githubClientSecret = process.env.GITHUB_CLIENT_SECRET;
}

const GithubState = props => {
  const initialState = {
    users: [],
    user: {},
    repos: [],
    loading: false
  };

  const [state, dispatch] = useReducer(GithubReducer, initialState);

  // Search Users
  const searchUsers = async text => {
    setLoading();

    const res = await axios.get(
      `https://api.github.com/search/users?q=${text}&client_id=${githubClientId}&client_secret=${githubClientSecret}`
    );

    dispatch({
      type: SEARCH_USERS,
      payload: res.data.items
    });
  };

  // Get User
  const getUser = async username => {
    setLoading();

    const res = await axios.get(
      `https://api.github.com/users/${username}?client_id=${githubClientId}&client_secret=${githubClientSecret}`
    );

    dispatch({
      type: GET_USER,
      payload: res.data
    });
  };

  // Get Repos
  const getUserRepos = async username => {
    setLoading();

    const res = await axios.get(
      `https://api.github.com/users/${username}/repos?per_page=5&sort=created:asc&client_id=${githubClientId}&client_secret=${githubClientSecret}`
    );

    dispatch({
      type: GET_REPOS,
      payload: res.data
    });
  };

  // Clear Users
  const clearUsers = () => dispatch({ type: CLEAR_USERS });

  // Set Loading
  const setLoading = () => dispatch({ type: SET_LOADING });

  return (
    <GithubContext.Provider
      value={{
        users: state.users,
        user: state.user,
        repos: state.repos,
        loading: state.loading,
        searchUsers,
        clearUsers,
        getUser,
        getUserRepos
      }}
    >
      {props.children}
    </GithubContext.Provider>
  );
};

export default GithubState;
```
#### 2. Enable netlify client to be running in the app.
```npm install -g netlify-cli```
#### 3. Create nelify.toml in the root directory
```
[build]
publish="build"
```
#### 4. Init netlify
```netlify init```
