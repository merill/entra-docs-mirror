---
layout: Conceptual
title: 'Tutorial: Add sign-in and sign-out components to a React single-page app (SPA) - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-single-page-app-react-configure-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to add authentication to a React single-page app (SPA) using the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2025-02-25T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: 7da92fd6-650e-e3d3-0002-b92ab0fca37f
document_version_independent_id: 7da92fd6-650e-e3d3-0002-b92ab0fca37f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-single-page-app-react-configure-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-single-page-app-react-configure-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-single-page-app-react-configure-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 54a368a2-32c6-ae5c-3aa5-8abb9daf96fd
---

# Tutorial: Add sign-in and sign-out components to a React single-page app (SPA) - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this tutorial you'll configure a React single-page application (SPA) for authentication. In [part 1 of this series](tutorial-single-page-app-react-prepare-app), you created a React SPA and prepared it for authentication. In this tutorial, you'll learn how to add authentication flows by adding [Microsoft Authentication Library (MSAL)](msal-overview) functional components to your app and build a responsive user interface (UI) for your app.

In this tutorial, you:

- Add functional components to the application
- Create a way of displaying the user's profile information
- Create a layout that displays the sign in and sign out experience
- Add the sign in and sign out experiences

## Prerequisites

- Completion of the prerequisites and steps in [Tutorial: Prepare an application for authentication](tutorial-single-page-app-react-prepare-app).

## Add functional components to the application

Functional components are the building blocks of React apps, and are used to build the sign-in and sign-out experiences in your application.

### Add the NavigationBar component

The navigation bar will provide the sign-in and sign-out experience for the app. The instance variable previously set in the *index.js* file will be used to call the sign-in and sign-out methods, which will redirect the user to the back to the sign-in page.

1. Open *src/components/NavigationBar.jsx* and add the following code snippet;

    ```jsx
    import { AuthenticatedTemplate, UnauthenticatedTemplate, useMsal } from '@azure/msal-react';
    import { Navbar, Button } from 'react-bootstrap';
    import { loginRequest } from '../authConfig';
    
    export const NavigationBar = () => {
        const { instance } = useMsal();
    
        const handleLoginRedirect = () => {
            instance.loginRedirect(loginRequest).catch((error) => console.log(error));
        };
    
        const handleLogoutRedirect = () => {
            instance.logoutRedirect().catch((error) => console.log(error));
        };
    
        /**
         * Most applications will need to conditionally render certain components based on whether a user is signed in or not.
         * msal-react provides 2 easy ways to do this. AuthenticatedTemplate and UnauthenticatedTemplate components will
         * only render their children if a user is authenticated or unauthenticated, respectively.
         */
        return (
            <>
                <Navbar bg="primary" variant="dark" className="navbarStyle">
                    <a className="navbar-brand" href="/">
                        Microsoft identity platform
                    </a>
                    <AuthenticatedTemplate>
                        <div className="collapse navbar-collapse justify-content-end">
                            <Button variant="warning" onClick={handleLogoutRedirect}>
                                Sign out
                            </Button>
                        </div>
                    </AuthenticatedTemplate>
                    <UnauthenticatedTemplate>
                        <div className="collapse navbar-collapse justify-content-end">
                            <Button onClick={handleLoginRedirect}>Sign in</Button>
                        </div>
                    </UnauthenticatedTemplate>
                </Navbar>
            </>
        );
    };
    ```
2. Save the file.

### Add the PageLayout component

The PageLayout component will be used to display the main content of the app and can be customized to include any additional content you want to display on every page of your app. The user's profile information will is displayed by passing the information via props.

1. Open *src/components/PageLayout.jsx* and add the following code snippet;

    ```jsx
    import { AuthenticatedTemplate } from '@azure/msal-react';
    
    import { NavigationBar } from './NavigationBar.jsx';
    
    export const PageLayout = (props) => {
        /**
         * Most applications will need to conditionally render certain components based on whether a user is signed in or not.
         * msal-react provides 2 easy ways to do this. AuthenticatedTemplate and UnauthenticatedTemplate components will
         * only render their children if a user is authenticated or unauthenticated, respectively.
         */
        return (
            <>
                <NavigationBar />
                <br />
                <h5>
                    <center>Welcome to the Microsoft Authentication Library For React Tutorial</center>
                </h5>
                <br />
                {props.children}
                <br />
                <AuthenticatedTemplate>
                    <footer>
                        <center>
                            How did we do?
                            <a
                                href="https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_ivMYEeUKlEq8CxnMPgdNZUNDlUTTk2NVNYQkZSSjdaTk5KT1o4V1VVNS4u"
                                rel="noopener noreferrer"
                                target="_blank"
                            >
                                {' '}
                                Share your experience!
                            </a>
                        </center>
                    </footer>
                </AuthenticatedTemplate>
            </>
        );
    }
    ```
2. Save the file.

### Add the DataDisplay component

The `DataDisplay` component will be used to display the user's profile information and a table of claims, which will be created in the next section of the tutorial. The `IdTokenData` component will be used to display the claims in the ID token.

1. Open *src/components/DataDisplay.jsx* and add the following code snippet;

    ```jsx
    import { Table } from 'react-bootstrap';
    import { createClaimsTable } from '../utils/claimUtils';
    
    import '../styles/App.css';
    
    export const IdTokenData = (props) => {
        const tokenClaims = createClaimsTable(props.idTokenClaims);
    
        const tableRow = Object.keys(tokenClaims).map((key, index) => {
            return (
                <tr key={key}>
                    {tokenClaims[key].map((claimItem) => (
                        <td key={claimItem}>{claimItem}</td>
                    ))}
                </tr>
            );
        });
        return (
            <>
                <div className="data-area-div">
                    <p>
                        See below the claims in your <strong> ID token </strong>. For more information, visit:{' '}
                        <span>
                            <a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/id-tokens#claims-in-an-id-token">
                                docs.microsoft.com
                            </a>
                        </span>
                    </p>
                    <div className="data-area-div">
                        <Table responsive striped bordered hover>
                            <thead>
                                <tr>
                                    <th>Claim</th>
                                    <th>Value</th>
                                    <th>Description</th>
                                </tr>
                            </thead>
                            <tbody>{tableRow}</tbody>
                        </Table>
                    </div>
                </div>
            </>
        );
    };
    ```
2. Save the file.