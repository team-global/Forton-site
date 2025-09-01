import "@stdlib/ownable";
import "@stdlib/deploy";
import "./messages.tact";

import "./ft_squad.tact";
import "./ft_user_storage.tact";
import "./ft_user_main.tact";
import "./ft_base_program_main.tact";

contract FtMaster with Deployable, Ownable {
    const minTonsForStorage: Int = ton("0.04");
    joinPrice: Int as coins = ton("3.0");
    squadPrice: Int as coins = ton("10.0");
    isSetup: Bool = false;

    index: Int as uint32;

    owner: Address;
    nextUserIndex: Int as uint64 = 1;
    programs: map<Int as uint8, Address>;

    init(index: Int) {
        self.index = index;
        self.owner = sender();
        self.deployBaseProgram();
    }

    receive(msg: SetupMaster){
        nativeThrowUnless(132, sender() == self.programs.get(0)!!);
        nativeThrowUnless(131, !self.isSetup);
        self.isSetup = true;

        self.registerUser(self.owner, 1);
    }

    receive(msg: SetupJoinPrice) {
        self.requireOwner();
        self.joinPrice = msg.newJoinPrice;
        self.reply("Join price successfully changed".asComment());
    }

     receive(msg: SetupSquadPrice) {
        self.requireOwner();
        self.squadPrice = msg.newSquadPrice;
        self.reply("Squad price successfully changed".asComment());
    }

    receive(msg: UpdateProgramAddress) {
        self.requireOwner();
        nativeThrowUnless(5, msg.programIndex > 0);
        self.programs.set(msg.programIndex, msg.programAddress);
    }

    receive(msg: GiftJoin) {
        let ctx: Context = context();
        let msgValue: Int = ctx.value;

        nativeThrowUnless(131, (msg.invitedId >= 1 && msg.invitedId < self.nextUserIndex));
        nativeThrowUnless(131, self.joinPrice <= msgValue);
        self.registerUser(msg.userAddress, msg.invitedId);
    }

    receive(msg: Join) {
        let ctx: Context = context();
        let msgValue: Int = ctx.value;

        if(msg.userAddress != null){
            let userStorageAddress: Address = self.userStorageAddress(msg.userAddress!!);
            nativeThrowUnless(132, sender() == userStorageAddress);
            self.createUser(userStorageAddress, msg.userAddress!!, msg.invitedId, msgValue);
        } else {
            nativeThrowUnless(131, (msg.invitedId >= 1 && msg.invitedId < self.nextUserIndex));
            nativeThrowUnless(131, self.joinPrice <= msgValue);
            self.registerUser(sender(), msg.invitedId);
        }
    }

    receive(msg: CreateSquad) {
        nativeThrowUnless(131, self.squadPrice + ton("0.5") <= context().value);
        let owner: Address = msg.owner == null ? sender() : msg.owner!!;
        self.createSquad(owner);
    }

    receive("GetProgramAddresses") {
        self.reply(
            ProgramAddresses{
                programs: self.programs
            }.toCell()
        );
    }

    // ------------------ Private Function  ------------------ //

    fun registerUser(userAddress: Address, invitedId: Int) {
        let init: StateInit = initOf FtUserStorage(userAddress, myAddress());
        send(SendParameters{
            to: contractAddress(init),
            value: 0,
            mode: SendIgnoreErrors | SendRemainingValue,
            body: VerifyExistence{
                invitedId: invitedId
            }.toCell(),
            code: init.code,
            data: init.data
        });
    }

    fun createUser(userStorageAddress: Address, userAddress: Address, invitedId: Int, value: Int) {
        let userId: Int = self.nextUserIndex;
        self.nextUserIndex = self.nextUserIndex + 1;
        let forwardPayload: Cell = SetupUserMain{owner: userAddress, invitedId: invitedId, programs: self.programs}.toCell();

        send(SendParameters{
            to: userStorageAddress,
            value: 0,
            mode: SendRemainingValue,
            body: SetupUserStorage{
                userId: userId,
                forwardPayload: forwardPayload
            }.toCell()
        });
    }

    fun createSquad(owner: Address){
        let init: StateInit = initOf FtSquad(owner, myAddress());
        nativeReserve(self.minTonsForStorage, 0);

        send(SendParameters{
            to: contractAddress(init),
            value: 0,
            mode: SendRemainingBalance,
            body: PayForSquadCreation{
                receiver: self.programs.get(0)!!,
                price: self.squadPrice
            }.toCell(),
            code: init.code,
            data: init.data
        });
    }

    fun deployBaseProgram(){
        nativeReserve(self.minTonsForStorage, 0);
        let init: StateInit = initOf FtBaseProgramMain(myAddress());
        let contractAddress: Address = contractAddress(init);
        self.programs.set(0, contractAddress);

        send(SendParameters{
            to: contractAddress,
            value: 0,
            mode: SendRemainingBalance,
            body: SetupBaseProgramMain {
                owner: self.owner
            }.toCell(),
            code: init.code,
            data: init.data
        });
    }
    
    // ------------------ Get Function  ------------------ //

    get fun balance(): Int {
        return myBalance();
    }

    get fun joinPrice(): Int {
        return self.joinPrice;
    }

    get fun squadPrice(): Int {
        return self.squadPrice;
    }

    get fun lastUserIndex(): Int {
        return self.nextUserIndex - 1;
    }

    get fun programs():  map<Int as uint8, Address> {
        return self.programs;
    }

    get fun userStorageAddress(address: Address): Address {
        let init: StateInit = initOf FtUserStorage(address, myAddress());
        return contractAddress(init);
    }

    get fun userMainAddress(id: Int): Address {
        let init: StateInit = initOf FtUserMain(id, myAddress());
        return contractAddress(init);
    }

    get fun userSquadAddress(address: Address): Address {
        let init: StateInit = initOf FtSquad(address, myAddress());
        return contractAddress(init);
    }
}
