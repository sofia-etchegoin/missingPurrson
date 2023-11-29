# Missing Purrson Documentation

### MVP

Cats can be fickle creatures and are known to occassionally take a hiatus. The heartache endured by their owners is all-consuming and leads to desperation. We've all seen posters stuck around of missing pets, their reach is limited, and hope wanes much like the sad paper that unpeels in the rain... Aside from conventional social media/forums, there's no dedicated online space to post about your awol-kitty troubles. A team of developers has taken it upon themselves to address this need. And so, we present Missing Purrson; the site to help cat owners reunite with their furry friends.

Our MVP will allow a user to:

- view a list of cats that are currently missing.
- use a form to upload a cat profile with details of their missing kitty (including a photo).
- view & record sightings of missing cats.

As stretch, our website will allow users to:

- pin the location of where they have sighted a missing cat on a map (using the Google Maps Api).
- register, login and logout of their account using auth0 authentication.

The tech we will use.

- Using the full-stack we have learnt at Dev Academy.
- Google maps Api.
- Auth0.
- Uploading images to database.

## Git workflow

Branches:
main -> dev -> 'front-end + descriptor' and 'back-end + descriptor'.

We will create pull requests to dev when features are finished on each branch. Anthony (Git Keeper) will manage the merges to dev.

The team will check whether:

- file and function naming conventions are maintained across the app
- errors are well handled
- no sensitive data is exposed on the client side
- it passes npm run lint without any code-related warnings or errors
- no unnecessary comments or console logs remain
- that Types are used where applicable, and any Type issues should be resolved
- user-facing updates (front end/ css crew) should be checked for accessibility concerns (using the WAVE tool) code meets naming conventions.

## Roles

- Scrum facilitator - Sofia
- Product Owner - Daniel
- Vibes Watcher - Ari
- Git Keeper - Anthony

We will divide the workload into front-end & back-end pairs, making sure to swap so that everyone can work on all layers of the stack. For now, the workload will be dividing as follows.

FRONT-END

- CSS/HTML - Daniel
- ReactQuery/Hooks - Daniel
- Components - Daniel
- Client-side rendering - Sofia
- ApiClient - Sofia

BACK-END

- Models - Anthony/Ari
- ApiClient - Anthony/Ari
- Server Routes - Ari
- Database - Anthony

STRETCH

- External Api (google maps Api) - Daniel
- Authentication - Sofia

## What might a day look like?

Turn up at 8:45am, start the day with a coffee and a standup. Set the daily KANBAN on the whiteboard. Take 5-10 mins in the morning and lunch to chat about the vibes. Work as a team to check the vibes during the day.

Lunch break at 12:30pm, taking regular breaks when needed. Allow for independent rest outside of Dev Academy during the day.

Provided we are clear on what we are doing (and not at meetings or taking breaks), we will be working on the tech during the day.

Post-lunch check-in (to make sure we are all on the same page.)

End of day retro to discuss what went well and what didn't.

## Link to designs/wireframes

https://www.figma.com/file/Zguxyv1UlY4WI6PdSUyk5q/Untitled?type=design&node-id=0%3A1&mode=design&t=6fiibhbiilWHnjfb-1

## Database

Link to the database diagram - https://dbdiagram.io/d/6565028d3be1495787d6d369

### Missing Cat Table

| COLUMN NAME          | DATA TYPE | PURPOSE                                   |
| -------------------- | --------- | ----------------------------------------- |
| foreign key (userId) | integer   | unique identifier                         |
| catId                | integer   | unique identifier for a missing cat       |
| userId               | integer   | unique identifier for the cat owner       |
| catName              | string    | name of the cat                           |
| breed                | string    | breed of the cat                          |
| color                | string    | color of the cat                          |
| description          | string    | description of the cat                    |
| dateLost             | string    | date the cat went missing                 |
| locationLat          | string    | latitude of the cat's last known location |
| locationLng          | string    | logitude of the cat's last known location |

### Users Table

| COLUMN NAME | DATA TYPE | PURPOSE                             |
| ----------- | --------- | ----------------------------------- |
| userId      | integer   | unique identifier for each user     |
| username    | string    | username from auth0 registration    |
| email       | string    | used to log into user account       |
| auth0_id    | string    | unique identifier supplied by auth0 |
| given_name  | string    | user's first name                   |
| family_name | string    | user's last name                    |

### Cat Images Table

| COLUMN NAME         | DATA TYPE | PURPOSE                                |
| ------------------- | --------- | -------------------------------------- |
| foreign key (catId) | integer   | unique identifier                      |
| imagesId            | integer   | unique identifier for a cat image      |
| catId               | integer   | unique identifier for a missing cat    |
| imageUrl            | string    | identifies which user saved the cheese |

### Sighted Cats Table

| COLUMN NAME          | DATA TYPE | PURPOSE                                   |
| -------------------- | --------- | ----------------------------------------- |
| foreign key (userId) | integer   | unique identifier                         |
| userId               | integer   | unique identifier for the cat owner       |
| catId                | integer   | unique identifier for a missing cat       |
| catName              | string    | name of the cat                           |
| breed                | string    | breed of the cat                          |
| color                | string    | color of the cat                          |
| description          | string    | description of the cat                    |
| dateLost             | string    | date the cat went missing                 |
| locationLat          | string    | latitude of the cat's last known location |
| locationLng          | string    | logitude of the cat's last known location |
| contactInfo          | string    | email?                                    |

## Naming conventions

| STACK LAYER | FILE/FOLDER NAME | FUNCTION NAME |
| ----------- | ---------------- | ------------- |
| Database    | db-cats.ts       | getAllCatsDb  |
| Database    | db-cats.ts       | getOneCatDb   |
| Database    | db-cats.ts       | addCatDb      |
| Database    | db-cats.ts       | deleteCatDb   |
| Database    | db-cats.ts       | updateCatDb   |
| Database    | db-users.ts      | getUsersDb    |
| Database    | db-users.ts      | getOneUserDb  |
| API Client  | api-cats.ts      | getAllCatsApi |
| API Client  | api-cats.ts      | getOneCatApi  |
| API Client  | api-cats.ts      | addCatApi     |
| API Client  | api-cats.ts      | deleteCatApi  |
| API Client  | api-cats.ts      | updateCatApi  |
| Component   | components       | App           |
| Component   | components       | Cat           |
| Component   | components       | DeleteCat     |
| Component   | components       | UpdateCat     |
| Component   | components       | SignIn        |
| Component   | components       | SignOut       |
| Component   | components       | Profile       |

## Server API endpoints

| METHOD | ENDPOINT                | PROTECTED? | USAGE                          | RETURNS                |
| ------ | ----------------------- | ---------- | ------------------------------ | ---------------------- |
| GET    | `/api/v1/cats`          | No         | gets a list of missing cats    | an array of cats       |
| GET    | `/api/v1/cats/:id`      | No         | gets an individual missing cat | an object              |
| POST   | `/api/v1/cats`          | Yes        | add a new missing cat          | the newly uploaded cat |
| DELETE | `/api/v1/cats/:id`      | Yes        | delete an existing cat         | nothing (status OK)    |
| PATCH  | `/api/v1/cats/:id`      | Yes        | update an existing cat         | the updated cat        |
| POST   | `/api/v1/auth/login`    | Yes        | log in a user                  | the user's JWT token   |
| POST   | `/api/v1/auth/register` | Yes        | register a user                | the user's JWT token   |

## Views Client Side

| PAGE               | MVP? | PURPOSE                                                                                                                                  |
| ------------------ | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Home               | yes  | welcomes the user, displays links to the 'list a missing cat' and 'missing cats' pages, and has login/register buttons in the top corner |
| Missing Cats       | yes  | shows images and some details of all the missing cats from the database that the user can click                                          |
| List a Missing Cat | yes  | shows a form to submit missing cat details and upload an image to the database                                                           |
| Cat Profile        | yes  | shows all the details of each missing cat (images, name, breed, age, last-seen/area, owner information)                                  |
| Cat Sighting       | yes  | allows a user to record whether they have seen a missing cat. Includes google map api as stretch                                         |
| Register           | no   | linked from the home page. View for the user to create an account                                                                        |
| Login              | no   | linked from the home page. View for the user to log into their account                                                                   |

## Authentication

To make a request to the server that checks the authentication of the user, use the custom hook `useAuthorisedRequest(method, endpoint, body)` which returns `<Promise<() => Promise<request.response>>>`

| Parameter | Data Type           | Purpose                                                   |
| --------- | ------------------- | --------------------------------------------------------- |
| method    | string              | the type of the request. `get` `post` `patch` or `delete` |
| endpoint  | string              | the endpoint of the request                               |
| body      | string or undefined | the body of the request                                   |

An example on how to create an authorised request:

```
//React Component function
export function CreateGetRequest() {

  // Use the hook at the top level of your component
  const makeRequest = useAuthorisedRequest('get', '/api/v1/auth', undefined)

  async function OnGetRequest() {

    // Make the request
    const response = await (await makeRequest)()
    // Output the response to console
    console.log(response)
  }

  return (
    // Only send an authorised request if the user is authenticated
    <IfAuthenticated>
      <button onClick={OnGetRequest}>Create get request</button>
    </IfAuthenticated>
  )
}
```

There are two example react components `SignIn` and `SignOut` that show how to sign the user in, out, and how to make an authenticated request. They should be placed as siblings in their parent component.

```
<SignIn/>
<SignOut/>
```

### Helper Components

There are two helper components that will render their children conditionally

```
// Will only render the <p> tag if the user is currently authenticated
<IfAuthenticated>
      <p>Currently signed in</p>
</IfAuthenticated>
```

```
// Will only render the <p> tag if the user is currently signed-out
<IfNotAuthenticated>
      <p>Currently signed out! Click here to sign in</p>
</IfNotAuthenticated>
```

## Human Skills - link to conflict resolution plan

https://docs.google.com/document/d/1yp-sKGSqoBdrwnCrR-KEHai1Pg_nWRAttEzwPM_fzLM/edit?pli=1