Virtual Vinli Routes
--------------------

Virtual Vinli uses pre-recorded drives, known as Dummy Routes, that can be virtually driven by Dummy Devices, simulating test data and various driving scenarios for your app.

List Dummy Routes
`````````````````

Request
+++++++

.. code-block:: json

  GET https://dummies.vin.li/api/v1/routes
  Accept: application/json

Response
++++++++
.. code-block:: json

  {
    "routes": [
      {
        "id": "8e90cf47-c6c1-486d-9ba8-194f569c7309",
        "name": "DFW - Back Home",
        "description": "DFW residential streets, start away and goes home quickly. Is the reverse of \"DFW - Home Loop 1 of 3\"; combine with that route to make a back and forth trip. Starts at (-96.783485, 32.834532). Will leave a geofence at that location with a 50m radius in Z seconds.  Will enter a second geofence at (-96.787547, 32.834541) in Z seconds. Stops at (-96.787547, 32.834541).",
        "messageCount": 28,
        "locationCount": 28,
        "distanceByGPS": 387.85,
        "distanceByVSS": 446.427,
        "duration": 86843,
        "preview": "y~kgEv_vmQLfBM|AB~@I~@Dt@AtHD~@ARGLD^AC",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/8e90cf47-c6c1-486d-9ba8-194f569c7309"
        }
      },
      {
        "id": "a9f09ad2-05d6-4b8d-b218-2e65a3229e8e",
        "name": "DFW - Circle the Block",
        "description": "Starts at (-96.787427, 32.83456)  will leave a geofence at that location with a 50m radius in Z seconds.  Will reenter same geo fence in Z seconds. Stops at (-96.787501, 32.834597).",
        "messageCount": 43,
        "locationCount": 43,
        "distanceByGPS": 588.761,
        "distanceByVSS": 625.607,
        "duration": 135665,
        "preview": "__lgElxvmQ@fAC`DJ|@_A^qAAe@LOk@A{CBwACaAB_@bCBbAEF\\Ih@OCCE",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/a9f09ad2-05d6-4b8d-b218-2e65a3229e8e"
        }
      },
      {
        "id": "64803498-cc0d-4724-99ef-e0d32d527670",
        "name": "DFW - Downtown Route 1",
        "description": "Out and about in downtown Dallas.  This route includes MAF and several other low-frequency parameters.",
        "messageCount": 139,
        "locationCount": 120,
        "distanceByGPS": 4506.49,
        "distanceByVSS": 8904.45,
        "duration": 499277,
        "preview": "wb_gElezmQ?wCm@sC{F}HiDiEq@uAsA}AeDsEyCgJKgCk@uDUaCa@cC_@kDYcFAiBOaCGeC_@eI_@oDi@wDiBgFw@wAuAiBqDeEaEmF_BaAoBq@cDSsB~BwApBsAdCaDpGyB`GuAtC{@`Dg@bIZ|Bn@hEOQJ?E?BbAN|@Nb@HbA\\~AFrBH`@LzAHf@r@LZAj@D\\Or@Cp@a@\\KCEABBDAEB?\\]g@}C]gCBDDEAEt@g@Rw@AWOm@V]G]MOOFCFBBDE@N?I",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/64803498-cc0d-4724-99ef-e0d32d527670"
        }
      },
      {
        "id": "7e582c36-281c-4551-b54a-0a49cadcb665",
        "name": "DFW - Downtown Route 2",
        "description": "Drives on city streets from the Omni hotel to local farmers market in Dallas",
        "messageCount": 88,
        "locationCount": 88,
        "distanceByGPS": 1718.89,
        "distanceByVSS": 1808.95,
        "duration": 1615955,
        "preview": "yp`gEj_zmQM?qAY[wAIkADy@WaCM{@Au@SqAO_BFs@Pm@?Y`@i@Zu@Lw@JcALw@J[n@Yz@Ql@Yd@s@pCoDn@q@jAwAGNBBEIHg@Oa@i@q@e@Uk@cBuAkBAGHBMGEKKKgAw@q@mAcA}@GOgAoAUc@u@q@Qe@iBsBs@o@CWOQc@aASq@CaADYFL",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/7e582c36-281c-4551-b54a-0a49cadcb665"
        }
      },
      {
        "id": "502361fb-a5aa-46c4-a565-064b7bea2ba1",
        "name": "DFW - Home Loop 1 of 3",
        "description": "DFW residential streets, first part of leaving home making two stops and returning home. Starts at (-96.787513, 32.834516). Will leave a geofence at that location with a 50m radius in Z seconds.  Will enter a second geofence at (-96.783492, 32.834472) in Z seconds. Stops at (-96.783492, 32.834472).",
        "messageCount": 39,
        "locationCount": 39,
        "distanceByGPS": 381.036,
        "distanceByVSS": 383.402,
        "duration": 123626,
        "preview": "w~kgE|xvmQDUB}@A{@NiCQ{@BaAEk@@kAG}BDiAFm@AYCA",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/502361fb-a5aa-46c4-a565-064b7bea2ba1"
        }
      },
      {
        "id": "072ef6be-688c-4116-bbcf-dd046531b648",
        "name": "DFW - Home Loop 2 of 3",
        "description": "DFW residential streets, second part of leaving home making two stops and returning home. Starts at (-96.783491, 32.834459). Will leave a geofence at that location with a 50m radius in Z seconds.  Will enter a second geofence at (-96.786937, 32.831146) in Z seconds. Stops at (-96.786937, 32.831146).",
        "messageCount": 38,
        "locationCount": 38,
        "distanceByGPS": 702.972,
        "distanceByVSS": 701.821,
        "duration": 119370,
        "preview": "k~kgEx_vmQ`B[p@B^A^ElA?z@Gl@FZKl@NhA@r@Ed@?JLNf@IdJN~BDlAAbAC\\C@AD",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/072ef6be-688c-4116-bbcf-dd046531b648"
        }
      },
      {
        "id": "377d7edc-ba9f-4d4c-a898-7c955f8d4eb6",
        "name": "DFW - Home Loop 3 of 3",
        "description": "DFW residential streets, third part of leaving home making two stops and returning home. Starts at (-96.786936, 32.831146). Will leave a geofence at that location with a 50m radius.  Will enter a second geofence at (-96.787518, 32.83455). Stops at (-96.787518, 32.83455).",
        "messageCount": 23,
        "locationCount": 23,
        "distanceByGPS": 416.802,
        "distanceByVSS": 436.012,
        "duration": 73684,
        "preview": "uikgEjuvmQADmCBo@DWEKH[Ho@HiEGcA?w@F]AQBEn@BNAJ",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/377d7edc-ba9f-4d4c-a898-7c955f8d4eb6"
        }
      },
      {
        "id": "3914d927-efae-43e8-9a00-5bffb1cae110",
        "name": "LAS - CES 1",
        "description": "200 locations in Southeast Las Vegas",
        "messageCount": 200,
        "locationCount": 200,
        "distanceByGPS": 13165.6,
        "distanceByVSS": 8558.36,
        "duration": 600001,
        "preview": "ufs{E`ik}T?fZyUZoAEmAKoB[eC{@cB}@aBiAyByBmBqAeAk@_Aa@iA]cB]aBOaCE_m@|@Jnd@@bPHnRHlc@c@Kyj@He@HM`SLaSh@RbRGpW?b@SlFA\\EbAF|@LrAVfA`@fAj@vAfA`DpDfA~@xA|@fBj@rAVn@BxDB?tZMp@@p|@CzE\\q@x@gAzBoCfDwDrAgBrHsIly@_aA]k@XYmAiBM]Gc@EmAGw@?a\\BkSBq@^eBd@w@hFgH\\w@Rs@N{@H_AD}BHw[CkY}X@",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/3914d927-efae-43e8-9a00-5bffb1cae110"
        }
      },
      {
        "id": "170820b0-fc2d-4ee6-aacd-88011d542545",
        "name": "Med Route - DFW",
        "description": "Out and about in Dallas",
        "messageCount": 277,
        "locationCount": 260,
        "distanceByGPS": 9357.61,
        "distanceByVSS": 9596.56,
        "duration": 957793,
        "preview": "wyhgEdeimQxDnCpBfEUpATnB~CdFbAl@l@bBVpBXhBz@~At@jArBbC`AtA|@vAfKxSjCxDhLzKh@Vn@JhDfAnBx@dA\\~FfEtGjO~@xAdFzC`ApBzAtA|AnAfAdA~@hBn@dBv@vAjAj@bB^z@d@Pz@JPnB~Ap@Z^pBb@|@Vb@r@d@\\l@bA|At@f@fIlIz@`ArClDn@|@jEdEp@d@j@n@Fh@?~@BvAF|ABzEDdBZpF\\xILfFLzC?rBDxBNxBfAvFXzB`@lBVl@Nn@`@xAnAjCH^VRp@bA\\Td@z@^hAXNb@b@Vd@^Tv@tAxBvBn@b@Ph@PZlAjBb@\\`@Tj@ThB`B|AjAr@VxA|@lBvA`ElDp@|@QvBa@`Au@|@y@LQJSnAM\\YZc@Xc@d@o@\\_AnBCj@FdApAfAd@vAn@lHFfBV|AJzAEhAJe@E?BMHF`@nAXtAFhARdBb@zBnAfNH|ABlBTfBfAjBEjE?jBPjB`@|Ag@n@~@d@x@x@z@lAd@|@v@lBXfAqCxAiBvAIIVM@SAHJOBZEG@CBBW^{@j@_A[GQA@EAG@EI\\RXHEUEV?XFQHER@ROD?BJKF[H@BDAKA",
        "links": {
          "self": "https://dummies.vin.li/api/v1/routes/170820b0-fc2d-4ee6-aacd-88011d542545"
        }
      }
    ],
    "meta": {
      "pagination": {
        "total": 9,
        "limit": 20,
        "offset": 0,
        "links": {
          "first": "https://dummies.vin.li/api/v1/routes?offset=0&limit=20",
          "last": "https://dummies.vin.li/api/v1/routes?offset=0&limit=20"
        }
      }
    }
  }
